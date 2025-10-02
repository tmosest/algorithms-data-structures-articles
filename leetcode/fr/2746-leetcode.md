---
titre: LeetCode 2746. Concaténation des chaînes décrémentales - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La concaténation des chaînes décrémentales – 2746
### Une solution complète Java / Python / C++ + SEO-Optimized Blog Post pour stimuler votre recherche d'emploi

---

Table des matières

Ce que vous apprendrez
- Oui.
Autres 1. Aperçu du problème Ce que le problème LeetCode demande réellement
Autres 2. Brute-Force vs DP. Pourquoi la solution naïve échoue et pourquoi DP brille
Autres 3. L'approche optimale du PDD – La conception, la transition et la mise en œuvre de l'État
Autres 4. Les erreurs hors-par-un, bouffées de mémoire, manipulation inutile des chaînes
Autres 5. L'Ugly – Edge Cases & Debugging Autres
Autres 6. Code multi-langue: Java, Python, C++ – les trois dans un seul fichier
Autres 7. SEO & Career Advices Comment cet article peut vous faire remarquer par les recruteurs
Autres 8. Feuille de triche rapide

---

- Oui. 1. Aperçu du problème

Code de Leet 2746 –** –
Étant donné un tableau `words[]` des chaînes `n` minuscules, nous devons effectuer des opérations de jointure `n‐1`:

- `join(x, y)` = `x + y` **à moins que** le dernier char de `x` égale le premier char de `y`; puis nous supprimons *un* de ces caractères dupliqués (la jointure produit encore une chaîne valide).
- À l'étape `i` nous pouvons soit ajouter `words[i]` après la chaîne actuelle ou la prépendre.

**Objectif**: minimiser la longueur de la corde concaténée finale.
«1 ≤ n ≤ 1000, 1 ≤=» mots[i]=» ≤ 50».

---

- Oui. 2. Brute-Force c. DP

L'approche Temps Espace Faisable ? Autres
- C'est quoi ?
Répertorier tous les 2^(n‐1) ordres d'adhésion + tenir la chaîne entière.
PDD over **full string** (mémoriser la chaîne exacte)
PD over **caractères de départ et de fin**

La principale perspicacité : le contenu *exact* de la chaîne intermédiaire n'a jamais d'importance, seulement ses premiers et derniers caractères et sa longueur. Pourquoi ?
Lorsque nous `join` deux cordes, le seul chevauchement possible est la paire de caractères *adjacents* – le dernier char de la chaîne gauche et le premier char de la chaîne droite. Tous les autres caractères ne sont pas affectés. Ainsi, un PDD tridimensionnel («dp[i][s][e]» est suffisant.

---

- Oui. 3. L'approche optimale du PDD

État

`dp[i][e]` – longueur minimale **extra** ajoutée par des mots concaténants `i ... n-1` si la chaîne de courant (déjà construite) commence par `s` et se termine par `e`.
- "s, e .. {0 ... 25}" (indices des lettres a.-z.).
- Oui. La longueur *total* à la fin est `totalSum – maxReduction`, où `totalSum` est la somme de toutes les longueurs de mots.
- `maxReduction` est le nombre de caractères dupliqués que nous avons réussi à supprimer.

Transition

Que le mot suivant soit `w = words[i]` avec le premier char `cs` et le dernier char `ce`.

1. **Appendir après** (chaîne actuelle + w)

- Nouveau départ = `s` (sans changement).
- Nouvelle fin = "ce".
- Si `e == cs`, nous supprimons un caractère duplicata.
- Sinon **0** duplicata.

2. **Prépendre avant** (w + chaîne actuelle)

- Nouveau départ = "cs".
- Nouvelle fin = "e".
- Si `ce= s`, nous supprimons un caractère en double **+1**.
- Sinon **0** duplicata.

Le DP choisit le nombre de duplicata *maximum* (parce que nous maximisons les suppressions, qui sont équivalentes à minimiser la longueur finale).

«» "
dp[i][s][e] = max(
(e==cs ? 1 : 0) + dp[i+1][s][ce],
(ce==s ? 1 : 0) + dp[i+1][cs][e]
)
«» "

Initialisation

`dp[0][firstWord][lastWord] = 0` – nous commençons par le premier mot; pas encore de duplications supplémentaires.

- Oui. Résultat

Après avoir rempli la table, la réponse est

«» "
minLength = totalSum - max(dp[0][premier][dernier] pour tous les premiers,derniers)
«» "

Parce que `dp[0][premier][dernier]` contient déjà les duplicatas *maximum* qui peuvent être réalisés lorsque le tableau entier est traité.

Complexité

- **Heure**: opérations "O(n · 262)" pour n=1000.
- **Espace**: même, environ 676 k entiers 3 Mo.

---

- Oui. 4. Les pièges communs

Pourquoi ça fait mal
- C'est quoi ?
**En utilisant des cordes entières** dans les touches DP.
**Indicateurs off-by-one** pour `i` dans la boucle.
** Supposons que la suppression réduit toujours la longueur**
**Utiliser la récursion sans mémoisation**
**Ne soustrayez pas 1 du totalSum** lorsqu'un duplicata est supprimé.

---

- Oui. 5. Les cas de bord et de débogage

Pourquoi ça compte ?
- C'est quoi ?
"n = 1"" Pas de jointure, réponse = "len(word0)" Vérifier le retour anticipé
Autres Mots qui commencent et se terminent par la même lettre (p. ex., "aaaa")
Dupliquer les lettres à l'intérieur d'un mot (p. ex., abba) Dupliquer les lettres à l'intérieur d'un mot (p. ex., abba)
Autres Tous les mots égaux à un seul caractère (-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Astuce de débogage**: imprimer `dp[i][s][e]` pour les petits `n` (= 5) et vérifier contre le dénombrement de force brute pour s'assurer que les transitions sont correctes.

---

- Oui. 6. Multi-langue Code

Ci-dessous vous trouverez **trois** solutions complètes et autonomes – une pour chacune des langues d'entrevue les plus populaires.

"'txt
# Nom du fichier: 2746_DecretalStringConcaténation.cpp
♪ Compiler: g++ -std=c++17 -O2 -pipe -statique -s -o sol 2746_DecretalStringConcaténation.cpp
Cours ! ./sol

*******************************************************************
* Code Leet 2746 – Décret Concaténation des chaînes
* PDD sur premier/dernier caractères (O(n·262))
* Code Java, Python & C++ dans un seul fichier
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// [En milliers de dollars des États-Unis] C++ [En milliers de dollars des États-Unis]
classe CppSolution {
public:
aut minimiserConcaténés Longueur(vecteur<chaîne> const& mots) {
int n = mots.size();
= 0;
pour (auto &w: mots) total += (int)w.size();

si (n == 1) retourner les mots[0].size();

// dp[i][s][e] = duplicata max de i.n-1 avec début s, fin e
groupe INF_NEG = -1e9;
vecteur <array<array<int,26>,26>> dp(n, {});
pour (int s=0;s<26;s++)
pour (int e=0;e<26;e++)
dp[0][s][e] = INF_NEG;

// Initialiser avec le premier mot
int fs = mots[0][0] - 'a';
int fe = mots[0].back() - 'a';
pour (int s=0;s<26;s++)
pour (int e=0;e<26;e++)
dp[0][s][e] = INF_NEG;
dp[0][fs][f] = 0; // pas encore de duplicata

pour (int i=1;i<n;i++) {
tableau <array<int,26>,26> ndp = dp[i-1];
pour (int s=0;s<26;s++)
pour (int e=0;e<26;e++)
ndp[s][e] = INF_NEG;

chaîne const& w = mots[i];
cs = w[0] - 'a';
int ce = w.back() - 'a';

pour (int s=0;s<26;s++) {
pour (int e=0;e<26;e++) {
Int cur = dp[i-1][s][e];
si (curs) INF_NEG continue;

// 1. Ajouter après
Int add1 = (e == cs) ? 1 : 0;
ndp[s][ce] = max(ndp[s][ce], cur + add1);

// 2. Préséance
int add2 = (ce == s) ? 1 : 0;
ndp[cs][e] = max(ndp[cs][e], cur + add2);
}
}
dp[i] = ndp;
}

int best = 0;
pour (int s=0;s<26;s++)
pour (int e=0;e<26;e++)
best = max(meilleur, dp[n-1][s][e];

total de retour - meilleur;
}
};

// [En milliers de dollars des États-Unis] Python [En milliers de dollars des États-Unis]
classe PythonSolution:
def minimiseConcaténées Longueur(self, mots: list[str]) -> Int:
n = len(mots)
total = somme(len(w) pour w en mots)
si n] 1 :
retour len(mots[0])

# dp[i][s][e] = duplicata max de i.n-1
dp = [[[ -1 pour _ dans l'intervalle(26)] pour _ dans l'intervalle(26)] pour _ dans l'intervalle(n)]
fs, fe = ord(mots[0]] - 97, ord(mots[0][-1]) - 97
dp[0][fs][f] = 0

pour i dans la plage (1, n):
cs, ce = ord(mots[i][0]) - 97, ord(mots[i][-1]) - 97
new_dp = [[-1]*26 pour _ dans l'intervalle(26)]
pour s dans la plage(26):
pour e dans la fourchette(26):
cur = dp[i-1][s][e]
Si cur == -1: continuer

# ajouter après
add1 = 1 si e == cs autre 0
new_dp[s][ce] = max(new_dp[s][ce], cur + add1)

# avant
add2 = 1 si ce == s autre 0
new_dp[cs][e] = max(new_dp[cs][e], cur + add2)

dp[i] = nouveau_dp

meilleur = 0
pour s dans la plage(26):
pour e dans la fourchette(26):
best = max(meilleur, dp[n-1][s][e])

total de retour - meilleur

♪ [En milliers de dollars des États-Unis] Java [En milliers de dollars des États-Unis]
/*
* Java 17 – Concaténation des chaînes décrémentales (LeetCode 2746)
* Heure: O(n · 262) Espace: O(n · 262)
*/
classe publique JavaSolution {
publique int minimiseConcaténé Longueur(mots de manche[]) {
int n = longueur de mots;
= 0;
pour (String w : mots) total += w.longueur();
si (n == 1) retourner les mots[0].longueur();

int[][] dp = nouvelle int[n][26][26];
pour (int i = 0; i < n; i++)
pour (int s = 0; s < 26; s++)
Les tableaux.fill(dp[i][s], -1);

int fs = mots[0].charAt(0) - 'a';
int fe = mots[0].charAt(mots[0].longueur() - 1) - "a";
dp[0][fs][f] = 0;

pour (int i = 1; i < n; i++) {
int cs = mots[i].charAt(0) - 'a';
int ce = words[i].charAt(words[i].longueur() - 1) - "a";
int[][] suivant = nouveau int[26][26];
pour (int s = 0; s < 26; s++)
les tableaux.fill(suivant[s], -1);

pour (int s = 0; s < 26; s++) {
pour (int e = 0; e < 26; e++) {
int cur = dp[i - 1][s][e];
si (curs) -1 continue;

// ajouter après
Int add1 = (e == cs) ? 1 : 0;
suivant[s][ce] = Math.max(suivant[s][ce], cur + add1);

// avant
int add2 = (ce == s) ? 1 : 0;
suivant[cs][e] = Math.max(next[cs][e], cur + add2);
}
dp[i] = suivant;
}

int best = 0;
pour (int s = 0; s < 26; s++)
pour (int e = 0; e < 26; e++)
best = Math.max(best, dp[n - 1][s][e]);

total de retour - meilleur;
}
}

// [En milliers de dollars des États-Unis] Chauffeur [En milliers de dollars des États-Unis]
Int main() {
// Démo C++
CppSolution cpp;
vector<string> words_cpp = {"ab", "ba", "ab"};
cout << "C++ réponse: " << cpp.minimizeConcaténatedLength(words_cpp) << "\n);

// Démo Python
PythonSolution py;
Liste <String> words_py = List.of("ab", "ba", "ab");
System.out.println("Réponse Python: " + py.minimizeConcatenatedLength(words_py));

// Démo Java
JavaSolution java;
Chaîne[] words_java = {"ab", "ba", "ab"};
System.out.println("Réponse de Java: " + java.minimizeConcatenatedLength(words_java));
}
«» "

**Note**: Pour la soumission réelle de LeetCode, téléchargez la classe pertinente (Java, Python ou C++) seule; le reste est juste pour votre commodité.

---

- Oui. 7. Que faire pour s'éloigner

1. **Transformer le problème**:
*À partir de* -Longueur minimale
*Pour* -maximiser les suppressions → plus simple DP.

2. **Keep DP indique un minimum**: premier/dernier caractères, pas des chaînes entières.

3. ** Maximiser les duplicata** (pas minimiser) dans le PDD pour obtenir la minimisation finale.

4. **Toujours double-vérifier** cas de bord avec force brute pour les petites entrées.

5. **Écrire un code propre et modulaire** – les solutions ci-dessus fonctionnent dans n'importe quel environnement de codage-challenge.

---

# # # 7.

- Utilisez un DP **2-D** sur les caractères `premier` et `dernier`.
- Transition ajoute une suppression seulement lorsque les chars de bord correspondent.
- Maximiser les suppressions → minimiser la longueur.
- La complexité est insignifiante pour n=1000: ~7 × 105 ops.
- Évitez les touches DP à chaîne entière; utilisez des tableaux entiers.

Bonne chance pour votre prochain entretien ! C'est ce qu'il a dit.
«» "

---

- Oui. 7. TL;DR (Traitement des entrevues)

1. **Insight clé**:
Réduisez l'état à seulement les premiers et derniers caractères de chaque mot.
2. **Formulation PD**:
Maximiser le nombre de suppressions (duplications) plutôt que de compter la longueur.
3. **Résultat**:
`finalLength = totalSum - maxDuplications`.
4. **Complexité**:
«O(n · 262)» temps et espace – s'adapte facilement aux contraintes de 1 seconde.

---

La pensée finale

La maîtrise de ce problème renforcera votre confiance dans la gestion des tâches *string DP*. La même approche (états → bords, max/min, DP itérative) peut être réutilisée pour d'autres problèmes de style de suppression maximale comme **swaps adjacents minimum** ou **concaténations optimales**.

Bon codage ! Les