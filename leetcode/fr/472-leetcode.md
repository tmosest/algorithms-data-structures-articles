---
titre: LeetCode 472. Mots concaténés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 472 – Mots concaténés
**Traitement : 1 k + solutions

---

### TL;DR
- **Objectif** – Trouvez chaque mot de la liste qui peut être construit à partir de *au moins deux* autres mots de la même liste.
- ** Solution classique** – Programmation dynamique (break-word) + un hash‐set pour les recherches O(1).
- **Langues** – Java, Python, C++ (voir le code ci-dessous).
- **Pourquoi ça compte** – Il teste votre capacité à raisonner sur **sous-problèmes**, **caching** et **caching-case-management**— compétences interviewers aiment.

---

- Oui. 1. Récapitulation des problèmes

Texte
Entrée: mots = ["cat", "cats", "catsdogcats", "dog", "dogcatsdog",
"hippopotames", "rat", "ratcatdogcat"]
Sortie: ["catsdogcats", "dogcatsdog", "ratcatdogcat"]
«» "

Un *mot concaténé* est une chaîne qui peut être segmentée en deux ou plus **mots plus courts** du même tableau (les mots plus courts peuvent être les mêmes).

Contraintes
- 1 ≤ longueur de mots ≤ 104
- 1 ≤ mots[i].longueur ≤ 30
- Tous les mots sont des lettres minuscules uniques
- Somme de toutes les longueurs ≤ 105

---

- Oui. 2. Pourquoi cette question est

C'est bien, c'est mal.
C'est pas vrai.
**Définition claire** – Vous n'avez qu'à vérifier la segmentation. Autres
**L'utilisation de la récursion** peut souffler la pile pour de longs mots. Autres
C'est vrai. **Peut être résolu dans n'importe quelle langue** – bon pour montrer la polyvalence. Autres

---

- Oui. 3. L'idée de base – PDD

1. **Trier les mots par la longueur** – nous assure toujours de construire des mots plus longs à partir de plus courts déjà vérifiés.
2. Conservez un `Set<String>` de tous les mots qui sont *valid* des mots concaténés ou des mots de base.
3. Pour chaque mot «w»:
- Exécutez un DP qui vérifie s'il peut être divisé en deux ou plusieurs mots de l'ensemble.
- Si `true`, ajouter `w` à l'ensemble et à la liste de réponses.
4. Retournez la liste de réponses.

Détails du DP

Que `dp[i]` soit `true` si le préfixe `w[0..i-1]` peuvent être segmentés.
Initialiser `dp[0] = true`.
Pour chaque `i` de `1` à `w.longueur`:
- Scanner tous les "j < i".
- Si "dp[j]] == true` **et** "w[j.i-1]" est dans le dictionnaire, set `dp[i] = true`.

À la fin, `dp[w.longueur]` nous dit si tout le mot peut être segmenté.
Nous devons également veiller à ce qu'au moins **deux** pièces soient utilisées: cela est naturellement satisfait parce que le DP commence par `dp[0]` et un seul mot ne définira jamais `dp[w.length] = true` à moins qu'il ne soit déjà dans l'ensemble.

Complexité

Opération Temps Espace
- C'est quoi ?
Ensemble de bâtiments
Tri de O(N log N)
(L ≤ 30)

Avec les contraintes ("sum(L) ≤ 105") cela s'inscrit facilement dans les limites.

---

- Oui. 4. Mise en œuvre des références

> Tous les codes sont **autocontenus**, comprennent les importations nécessaires et sont prêts à fonctionner sur LeetCode.

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe {
liste publique<String> trouver tous les motsConcaténésInADict(String[] mots) {
Liste du résultat <String> = nouvelle liste de distribution<>();
Définir <String> dict = nouveau HashSet<>();
// Trier les mots par longueur ascendante
Arrays.sort(mots, Comparator.comparingInt(String::longueur));

pour (Mot d'ordre : mots) {
si (word.isEmpty()) continue; // défensive
si (canForm(word, dic)) result.add(word);
dict.add(mot); // mot devient un bloc de construction
}
le résultat du retour;
}

boîte de booléenne privéeFormer(mot de la chaîne, définir<String> dic) {
si (dict.isEmpty()) retourne faux;
int n = mot.longueur();
booléen[] dp = nouveau booléen[n + 1];
dp[0] = vrai;
pour (int i = 1; i <= n; i++) {
pour (int j = 0; j < i; j++) {
si (!dp[j]) continue;
si (dict.contient(word.substring(j, i)) {
dp[i] = vrai;
break; // trouvé une scission, pas besoin de vérifier plus j's
}
}
}
retour dp[n];
}
}
«» "

> **Pourquoi cela fonctionne** – Le jeu ne contient que des mots * strictement plus courts * que le courant parce que nous trions par longueur.
> **Edge-case** – Si le mot lui-même est déjà dans l'ensemble (en raison d'une entrée dupliquée, ce que le problème interdit), l'algorithme ne retournera `true` que s'il peut être segmenté en utilisant d'autres mots.

---

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def findAllConcatenated MotsInADict(self, mots: List[str]) -> Liste[str]:
mots.sort(key=len)
résultat, dictionnaire = [], set()

pour mot en mots:
sinon mot: # garde de sécurité
poursuivre
if self._can_form(mot, dictionnaire):
result.append(mot)
dictionnaire.add(mot)

résultat du retour

def _can_form(self, mot: str, dictionnaire: set) -> C'est vrai.
si non dictionnaire:
Retour Faux
n, dp = len(mot), [False] * (n + 1)
dp[0] = Vrai
pour i dans la plage(1, n + 1):
pour j dans la plage i:
si ce n'est pas dp[j]:
poursuivre
si mot[j:i] dans le dictionnaire:
dp[i] = Vrai
pause
retour dp[n]
«» "

> **Conseils spécifiques au python** –
> * Utilisez `word[j:i]` slicing – c'est O(1) en raison de l'implémentation sous-chaîne Python.
> * La boucle intérieure sort tôt avec `break` une fois qu'une scission est trouvée – cela maintient l'exécution faible.

---

### 4.3 C++

'`cpp
#incluez <vecteur>
#incluez <string>
#inclut <unordered_set>
#incluez <algorithme>

solution de classe {
public:
md::vecteur<std::chaîne> findAllConcatenatedWordsInADict(std::vector<std::string>& words) {
md::vecteur<std::chaîne> résultat;
std::unordered_set<std::string> Le décret;

// Trier les mots par longueur (croissante)
std::sort(words.begin(), words.end(),
[](suite::string& a, const st::string& b) {
retourner a.size() < b.size();
});

pour (suite::string& mot: mots) {
si (word.vide()) continue; // garde défensive
si (canForm(word, dict)) result.push_back(word);
dict.insert(mot); // mot devient un bloc de construction
}
le résultat du retour;
}

particulier:
bool canForm(const std::string& word, const std::unordered_set<std::string>& dict) {
si (dict.vide()) retourne faux;
int n = mot.size();
std::vector<bool> dp(n + 1, false);
dp[0] = vrai;

pour (int i = 1; i <= n; ++i) {
pour (int j = 0; j < i; ++j) {
si (!dp[j]) continue;
si (dict.find(word.substr(j, i - j)) !=dict.end()) {
dp[i] = vrai;
rupture; // trouvé une rupture
}
}
}
retour dp[n];
}
};
«» "

> **C++ note** – `word.substr(j, i - j)` crée une nouvelle chaîne à chaque fois; cependant, puisque la longueur du mot ≤ 30 est négligeable.
> Si vous avez besoin d'une micro-optimisation absolue, vous pouvez implémenter une Trie et éviter les sous-chaînes.

---

- Oui. 5. Conseils d'entrevue

Conseil Pourquoi c'est important
-- -- -- -- --
**Dépliez l'étape de tri**Démontre que vous comprenez la *dépendance* (les mots plus longs dépendent de plus courts). Autres
**Afficher le tableau du DP** Autres
**Discuss edge-cases**. Chaîne vide, mots simples, duplicata (même si les contraintes interdisent). Autres
**Complexité temps/espace** Les intervieweurs s'attendent à ce que vous expliquiez pourquoi votre solution est efficace. Autres
Autres **Si vous êtes coincé, posez des questions de clarification**. Cela démontre des compétences en résolution de problèmes. Autres

---

- Oui. 6. Aperçu du blog optimisé SEO

> *Utilisez cette esquisse sur votre blog personnel ou votre portfolio pour classer pour le problème d'entrevue de Java DP. *

1. **Titre** –
`LeetCode 472 – Concaténé Mots : Problème dur expliqué (Java/Python/C++) "

2. **Description détaillée** –
`Solve LeetCode 472 – trouver tous les mots concaténés dans un dictionnaire. Lisez les solutions détaillées Java, Python et C++, ainsi que les conseils d'entrevue et l'analyse de complexité temporelle. Boostez vos compétences d'entrevue de codage maintenant! "

3. **En-têtes**
LeetCode 472 – Concaténé Mots: dur problème "
- Oui. Énoncé des problèmes et contraintes "
- Oui. Pourquoi cette question est difficile'
- Oui. La stratégie du PDD en bref "
- Oui. Analyse de complexité "
- Oui. Solutions de référence "
- Oui. Mise en œuvre Java "
- Mise en œuvre de Python "
- Oui. C++ Mise en œuvre "
- Oui. Discussion sur la préparation à l'entrevue "
- Oui. A emporter & Lecture supplémentaire "

4. ** Liens internes et externes* *
- Lien vers `https://leetcode.com/problems/concaté-words/`
- Lien vers votre repo GitHub contenant le code.
- Référencer d'autres problèmes de DP dur de LeetCode (par exemple, 139 :

5. **Appel à l'action** –
Vous voulez plus d'entrevues ? Abonnez-vous à l'hebdomadaire LeetCode. "

---

- Oui. 7. Dernier départ

- **Traitement par longueur** + **DP :
- Oui. La question vous oblige à penser **à l'ordre de dépendance** et **à la gestion des cas de base**, qui sont critiques lors de toute entrevue difficile avec le DP.
- Avec les trois variantes linguistiques, vous êtes prêt à présenter à la fois la perspicacité algorithmique et la fluidité de la langue – une entrée de portefeuille idéale pour les entrevues de génie logiciel senior.

Bon codage, et que votre pile d'entrevue soit toujours vraie!

---


> *Si vous voulez en savoir plus sur les modèles DP, consultez notre série sur LeetCode . *

---

*Auteur: [Votre nom] – Ingénieur logiciel et coach d'entrevue.
Mots clés : LeetCode 472, Mots concaténés, Problème de DP dur, Java DP, Python DP, C++ DP, Conseils d'entrevue. *
---


> **TL;DR** – Tri, DP, ensemble. Trois solutions prêtes à coller. Explication prête à l'entrevue ci-dessus. C'est ce qu'il a dit.
---
Ceci vient compléter le code de Leet 472 – Mots concaténés** plongée profonde, avec **code de référence** et **préparation d'entrevue** prêt pour votre prochaine entrevue de codage.