---
titre: LeetCode 2052. Coût minimum pour séparer les peines dans les lignes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code

Voici des solutions propres et prêtes à la production pour LeetCode 2052 – *Coût minimum pour séparer les peines dans les lignes*.
Chaque implémentation suit la même idée DP mais utilise le style idiomatique de la langue choisie.

> **Astuce** – La limite de temps sur LeetCode pour ce problème est généreuse, mais si vous voulez être en sécurité sur de très grandes entrées, utilisez le **O(n2)** DP avec mémorisation ou table ascendante.
> **Espace** – Les trois solutions fonctionnent dans *O(n)* espace auxiliaire (hors tableau de sortie).

#### 1.1 Java – Haut Mémotisation descendante

"Java
Importation de java.util.*;

solution de classe publique {
// mémo[i] = coût minimum à partir du mot i
Int privé[] mémo;

Int minimum public Coût(Pendant, int k) {
Chaîne[] mots = phrase.split(");
int n = longueur de mots;
mémo = nouvelle int[n];
Tableau.fill(memo, -1); // -1 = non calculé
retourner dfs(0, mots, k);
}

Int privé dfs(int i, String[] mots, int k) {
si (i >= mot.longueur) retourne 0; // atteint fin – dernier coût de ligne 0

Si (memo[i] != -1) retourner le mémo[i];

int lineLen = k; // caractères laissés dans la ligne courante
int best = entier.MAX_VALUE;

pour (int j = i; j < words.longueur; j++) {
lineLen -= words[j].length(); // place word j
Si (ligneLen < 0) pause; // ne peut pas correspondre à plus de mots

coût int = (j == words.longueur - 1) ? 0 : ligneLen * ligne Len;
best = Math.min(best, coût + dfs(j + 1, mots, k));

lineLen--; // compte pour l'espace après mot j
}
mémo[i] = meilleur;
le meilleur retour;
}
}
«» "

* Pourquoi ça marche : *
La fonction récursive essaie tous les points de rupture possibles après le mot actuel "i".
Si nous terminons la phrase, aucun coût n'est ajouté pour la dernière ligne (par définition).
Le tableau de mémos garantit que chaque index de départ n'est évalué qu'une seule fois, ce qui donne une complexité temporelle **O(n2)**.

---

#### 1.2 Python – `functools.lru_cache` (Top-Down)

'`python
à partir de functools importer lru_cache
importations

Solution de classe:
def minimum Coût(self, phrase: str, k: int) -> Int:
mots = phrase.split()
n = len(mots)

@lru_cache(Aucun)
def dp(i: int) -> Int:
Si i == n:
retour 0 # dernière ligne – coût 0

restant = k
best = sys.maxsize

pour j dans la plage(i, n):
restant -= len(mots[j])
s ' il reste < 0:
break # ne peut pas ajouter plus de mots
# coût de cette ligne (sauf la dernière)
Coût = 0 si j == n - 1 autre restant * restant
best = min(meilleur, coût + dp(j + 1))
restant -= 1 # espace après les mots[j]

le meilleur retour

retour dp(0)
«» "

* Pourquoi ça marche : *
Le décorateur `lru_cache` nous donne gratuitement des mémos.
Nous partons sur tous les points de rupture possibles du mot actuel "i".
La dernière ligne reçoit un coût de « 0 ».
L'algorithme fonctionne dans l'espace *O(n2)* et *O(n*).

---

### 1.3 C++ – PDD ascendant

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimum Coût(pilule chaîne, int k) {
vecteur <string> les mots;
chaîne w;
ss(sentence);
pendant (ss >> w) words.push_back(w);

int n = mots.size();
INF = 1e9;
vecteur<int> dp(n + 1, INF);
dp[n] = 0; // base: après le dernier mot

pour (int i = n - 1; i >= 0; --i) {
la ligne intLen = k;
pour (int j = i; j < n; ++j) {
lineLen -= mots[j].size();
si (ligneLen < 0) pause; // plus de mots

coût int = (j == n - 1) ? 0 : ligneLen * ligne Len;
dp[i] = min(dp[i], coût + dp[j + 1];

ligne Len-; // espace après mots[j]
}
}
retour dp[0];
}
};
«» "

* Pourquoi ça marche : *
La boucle ascendante reflète la récursion supérieure vers le bas, mais évite les récursions aériennes.
«dp[i]» stocke le coût minimum du mot `i` à la fin.
La boucle interne essaie tous les points de rupture suivants valides.
Le résultat est dans `dp[0]`.
La complexité est de nouveau **O(n2)** temps, **O(n)** espace.

---

- Oui. 2. Article de blog: Le bon, le mauvais, et le mauvais de LeetCode 2052

2.1 Introduction

**LeetCode 2052 – Le coût minimal pour séparer la peine dans les lignes** est un problème classique **de programmation dynamique** qui teste votre capacité à optimiser avec les fonctions *pénales*.
Il s'agit d'une question d'entrevue parfaite pour les rôles de niveau intermédiaire dans le génie logiciel, les sciences des données ou les positions centrées sur l'algorithme.

> **Mots-clés de référence** – Coût minimum pour séparer les peines dans les lignes, LeetCode 2052, programmation dynamique, Java, Python, C++, entretien de codage, conception d'algorithmes, préparation d'entretiens d'emploi, défi de codage.

2.2 Récapitulation du problème

Vous avez reçu :
- Une phrase de mots minuscules séparés par un seul espace.
- Une largeur maximale de rangée "k".

**Objectif** – Diviser la phrase en lignes de sorte que chaque ligne ait au plus des caractères `k` (espaces comptés).
Le coût d'une ligne non-dernière est `(k - lineLength)2`.
Retournez le *coût total minimum*.

### 2.3 Le bon – Ce qui fonctionne hors de la boîte

Aspect Pourquoi c'est bon
C'est pas vrai.
**Espace linéaire** Chaque implémentation ne conserve que l'état « O(n) » – la table de mémos ou le tableau DP. Autres
**Récurrence intuitive**=Essayez toutes les ruptures possibles de la prochaine ligne. Autres
**Aucune bibliothèque supplémentaire**= Les solutions ne s'appuient que sur des bibliothèques standard (Java=s `Arrays`, Python=s `functools`, C++ STL). Autres
Avec `n <= 5000`, le 'O(n2)` DP (=25 millions d'itérations) s'inscrit confortablement dans les délais typiques du LeetCode. Autres

2.4 Les mauvaises – Pièges communs

Piège
- Oui.
**Off‐by‐One Erreurs dans les espaces**= N'oubliez pas de soustraire 1 pour l'espace *après* chaque mot **sauf** le dernier mot de la ligne. Autres
**Coût pour la dernière ligne**= De nombreux codeurs ajoutent par erreur `(k - lineLen)2` pour la dernière ligne. La déclaration dit **, sauf le dernier**. Autres
**Large Récursion Profondeur**.Dans les langues avec pile limitée (Python, Java), la récursion profonde (`n=5000`) peut déborder. Utilisez `@lru_cache` ou DP itératif. Autres
Autres **Types de données erronés**= Le coût peut atteindre `k2` (25 millions de dollars). Dans les langues 32 bits, `int` est très bien, mais attention à déborder dans des langues comme C# ou lorsque vous utilisez des entiers 32 bits dans d'autres contextes. Autres

#### 2.5 L'horrible – Morceaux d'ombres

1. **Sentences en un mot**
*Cas:* `"a"` avec `k = 5`.
* Comportement:* Une seule ligne – le coût devrait être `0`.
*Bug:* Certaines implémentations DP traitent `k - lineLen` comme `0` pour la seule ligne, ce qui entraîne un coût *faux* positif.

2. **Durée du mot exactement "k"**
*Cas:* `"abcdefgh"` avec `k = 8`.
* Comportement:* Doit être sur sa propre ligne; coût `0`.
*Bug:* Ne pas rendre compte de l'espace* après le mot peut causer un débordement de la longueur de la ligne.

3. ** Taille maximale**
*Case:* "sentence.longueur = 5000", tous les mots de longueur 1.
*Complexité:* `n2` ~ 25M itérations; Python peut être lent si ne pas utiliser `lru_cache`.
*Optimisation:* Utilisez `sys.setrecursionlimit(10000)` ou un DP itératif ascendant dans Python.

#### 2.6 La récurrence du PDD – Une marche pas à pas

Laissez `words` être un tableau des mots de phrase, `n = words.length`.
Définissez `dp[i]` = coût minimum pour la sub-sentence commençant par le mot `i`.
Base: `dp[n] = 0` (aucun mot gauche → dernière ligne, coût 0).

Pour `i` de `n-1` jusqu'à `0`:

1. `lineLen = k` (caractères restant dans la ligne actuelle).
2. Pour chaque `j` de `i` à `n-1`:
- Soustraire la longueur des mots de "lineLen".
- Si 'lineLen < 0', casser (ne peut pas s'adapter).
- Calculer `cost = (lineLen)2` si `j != n-1` autre `0`.
- Mettre à jour `dp[i] = min(dp[i], coût + dp[j+1])`.
- Décret `lineLen` par `1` pour rendre compte de l'espace qui suivrait `words[j]`.

Retour `dp[0]`.

**Pourquoi la récurrence est correcte? * *
Chaque décision choisit un point d'arrêt après le mot "j".
Le coût de la ligne est entièrement déterminé par les caractères restants (`k - lineLen`).
L'ajout du coût optimal du suffixe restant (`dp[j+1]`) garantit l'optimalité par le principe de la substructure optimale.

2.7 Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Mémoisation top-down (Java, Python)
(C++, Java, Python)

Avec `n ≤ 5000`, les opérations les plus difficiles sont d'environ 25 millions – confortablement dans les limites d'une seconde pour les juges modernes.

2.8 Essais et validation

Autres Description du test
- C'est quoi ?
"("I love leetcode", 12)" Exemple
"("les pommes et les bananes ont bon goût", 7)" Exemple
Mot unique
"("abcdefgh", 8)""Le mot correspond exactement à" 0"
De nombreux mots courts
"("a b c d e f g h i j", 10)" Cas de bord

Automatisez ces vérifications dans vos tests unitaires ; n'oubliez pas de modifier l'ordre des fractionnements de mots pour vérifier votre manipulation des espaces.

####2.9 Conseils pour l'entrevue

1. **Exposer clairement la récurrence** – Montrer le principe de la sous-structure optimale.
2. **Address Edge Cases Early** – Mettez en évidence la façon dont vous manipulez la règle du coût de la dernière ligne.
3. **Mention Space Complexity** – Les intervieweurs se soucient souvent de l'utilisation de la mémoire autant que de l'exécution.
4. **Si vous utilisez la récursion, montrez l'option itérative** – Mentionnez que vous pouvez refactorer vers le haut si la profondeur de récursion est une préoccupation.
5. **Complexité temporelle** – Parlez de `O(n2)` et pourquoi il est acceptable sous les contraintes.
6. **Discuses Optimisations potentielles** – Par exemple, pré-calculer des montants de longueurs de mots pour éviter les répétitions de «len()» appels.

2.10 Dernier départ

LeetCode 2052 est un problème PD ** propre et bien structuré** qui, une fois résolu correctement, démontre votre capacité à:
- Traduire un problème de mot en une récurrence algorithmique.
- Gérer soigneusement les erreurs hors-par-un.
- Optimiser dans des limites strictes.

Utilisez les extraits de code **** ci-dessus comme référence.
Pratiquer sur des problèmes similaires de formatage basés sur la Pénalité (p. ex., ** Justification du texte** ou **Word Wrap**) pour approfondir votre intuition.

Bonne chance pour votre prochain entretien de codage !

---

*L'article met en balance la clarté, les conseils pratiques et le langage prêt à l'entrevue, ce qui le rend idéal pour les demandeurs d'emploi qui veulent présenter leurs prouesses algorithmiques aux recruteurs et aux gestionnaires d'embauche. *