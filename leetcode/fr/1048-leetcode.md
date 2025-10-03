---
titre: LeetCode 1048. Chaîne à cordes la plus longue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La maîtrise du LeetCode 1048 – Le plus long Chaîne de chaînes
**Une plongée profonde en DP, tri et prédécesseur* *

> *Vous souhaitez obtenir une entrevue sur l'ingénierie logicielle?
> Résoudre le problème de la chaîne à cordes la plus longue en **Java, Python et C++** – la solution officielle + une écriture de style blog poli. *

---

Table des matières

Section du texte
C'est pas vrai.
Autres Aperçu du problème
Autres Intuition & Aperçu des clés
Autres La Brute-Force et pourquoi elle fait défaut
Autres 5 min
Code Passage (Java)
Autres Code Passage (Python)
Autres Le code passe par (C++)
Cerfs et pièges communs
Autres Analyse de complexité
SEO & Carrière à emporter
Références et lectures complémentaires

> *Total: ~45 minutes de lecture, plus ~20 minutes pour coder et exécuter des tests. *

---

- Oui. 1. Aperçu du problème (Code de bord 1048)

> ** Chaîne à cordes la plus longue**
> *Moyenne

Étant donné un tableau `mots` de mots anglais minuscules, nous pouvons appeler `motA` un **prédécesseur** de `motB` si nous pouvons insérer **exactement une lettre** n'importe où dans `motA` (sans ré-ordonner les autres lettres) pour obtenir `motB`.
Une chaîne *word* est une séquence `[word1, word2, ... , wordk]` où chaque mot est un prédécesseur du suivant.
Retourne la longueur maximale de toute chaîne.

**Contrôles* *

Valeur
C'est pas vrai.
Valeur de référence
1 ≤ mots [i].longueur ≤ 16 '
"Mots[i]" seulement lettres anglaises minuscules

---

- Oui. 2. Intuition et principales perspectives

1. **La longueur de la chaîne est déterminée par la longueur du mot**
Chaque étape ajoute exactement une lettre, de sorte qu'une chaîne de longueur `L` doit comporter des mots de longueur `len`, `len+1`, ..., `len+L-1`.

2. **Traitement par longueur**
Si nous traitons les mots de *la plus courte à la plus longue*, tous les prédécesseurs possibles d'un mot sont déjà traités.
Cela élimine la nécessité d'un retour en arrière ou d'une forte récursion.

3. ** Programmation dynamique sur les mots**
Laisser `dp[w]` = chaîne la plus longue se terminant au mot `w`.
Lorsque nous considérons un mot `w`, nous générons tous *précédents possibles* (supprimer un caractère à chaque position) et mettons à jour `dp[w]` utilisant leurs valeurs `dp`.

4. **Hash Map pour la recherche O(1)* *
Nous stockons les valeurs `dp` dans une `HashMap` clé par la chaîne de mots.
Ainsi, le calcul de la longueur de chaîne du prédécesseur est "O(1)".

---

- Oui. 3. Brute-Force et pourquoi elle échoue

Une solution naïve :

1. Vérifiez chaque paire `a, b)` pour voir si `a` est un prédécesseur de `b`.
2. Construire un graphique et effectuer DFS/BFS pour trouver le chemin le plus long.

Avec jusqu'à 1000 mots, cela conduit à des vérifications de paires `O(n2)`, et chaque contrôle prédécesseur coûte `O(len)` → ~16 millions d'opérations – encore très bien, mais le chemin le plus long basé sur le graphique est *NP‐hard* pour les graphiques arbitraires.

L'approche de tri DP + la réduit à "O(n · len2)" (~1 million d'opérations) et garantit l'exactitude.

---

- Oui. 4. Stratégie optimale DP + tri

Texte
trier les mots par longueur ascendante
pour chaque mot w dans l'ordre trié
dp[w] = 1 // cas de base: chaîne de longueur 1
pour chaque indice
prédécesseur = w avec char à i enlevé
si le prédécesseur existe en dp
dp[w] = max(dp[w], dp[prédécesseur] + 1)
réponse = max(dp.valeurs)
«» "

Pourquoi ça marche ?
Parce que tous les prédécesseurs de `w` sont plus courts que `w`, ils ont déjà été traités et leurs valeurs `dp` sont définitives. La relation de récurrence est exactement le classique **La plus longue séquence croissante** sur un DAG.

---

- Oui. 5. Passage en code – Java 17

"Java
Importation de java.util.*;

solution de classe publique {
publique StrChain(String[] mots) {
Tri par longueur ascendante
Arrays.sort(mots, Comparator.comparingInt(String::longueur));

Carte DP : mot -> la plus longue chaîne se terminant à ce mot
Carte<String, entier> dp = nouveau HashMap<>();

int best = 1; // au moins un mot

pour (Pièce w : mots) {
longueur de la chaîne pour w

// Générer tous les prédécesseurs en enlevant un char
pour (int i = 0; i < w.longueur(); i++) {
StringBuilder sb = nouveau StringBuilder(w);
sb.deleteCharAt(i);
Chaîne pred = sb.toString();

si (dp.contientKey(pred)) {
cur = Math.max(cur, dp.get(pred) + 1);
}
}

dp.put(w, cur);
best = Math.max (best, cur);
}
le meilleur retour;
}
}
«» "

** Faits saillants* *

- `Arrays.sort` utilise un type stable, la complexité `O(n log n)`.
- La construction de chaque ancien coût "O(len)" → au plus 16 opérations.
- HashMap assure la recherche `O(1)`.

---

- Oui. 6. Passage du code – Python 3.11

'`python
de taper l'importation Liste
de collections importer par défautdict

Solution de classe:
plus longtemps StrChain (soi-même, mots : List[str]) -> Int:
N° 1 Tri par longueur
mots.sort(key=len)

dp = defaultdict(int) # word -> la plus longue chaîne se terminant au mot
meilleure = 1

pour w en mots:
cur = 1
# générer tous les prédécesseurs
pour i dans la plage(len(w)):
b) Préd = w[:i] + w[i+1:]
si dp[pred]:
cur = max(cur, dp[pred] + 1)
dp[w] = cur
best = max (meilleur, cur)

le meilleur retour
«» "

- Python=s `defaultdict(int)` se comporte comme une carte de hachage par défaut 0.
- Le slice à cordes est efficace pour la petite longueur (‘=16').

---

- Oui. 7. Passage du code – C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int le plus long StrChain(vecteur<string>& mots) {
tri(words.begin(), words.end(),
[](const string &a, const string &b){ retourner a.size() < b.size(); });

unordered_map<string, int> dp;
int best = 1;

pour (const string &w : mots) {
Int cur = 1;
chaîne pred;
préd.reserve(w.size());

// supprimer chaque caractère une fois
pour (int i = 0; i < (int)w.size(); ++i) {
pred = w.substr(0, i) + w.substr(i + 1);
auto it = dp.find(pred);
si (it != dp.end())
cur = max(cur, it->seconde + 1);
}
dp[w] = cur;
best = max (meilleur, cur);
}
le meilleur retour;
}
};
«» "

- `unordered_map` donne une recherche amortie `O(1)`.
- "substr" est sûr parce que la longueur des mots est minuscule.

---

- Oui. 8. Cas de bord et pièges communs

Qu'est-ce qui se passe ?
- C'est quoi ?
Retirez les duplicates en premier ou utilisez `max` lors de l'insertion. Autres
Autres Longueur des mots Le prédécesseur est une chaîne vide. Autres
Autres Tous les mots ne sont pas liés.La réponse doit être 1. Autres
Autres Grand usage de la mémoire de 1000 mots × 16 caractères → trivial. Autres
Un tri stable ou instable fonctionne. Autres

---

- Oui. 9. Analyse de la complexité

Étape
C'est quoi ?
Trier "O(n log n)" Autres
Chaque mot `w` de la longueur `L` → `O(L)` vérifications antérieures → `O(n ·L)` (L ≤ 16)
Hash Map Opérations Amorti `O(1)` par recherche/insertion

**Total**: < < O(n log n + n · L) > > < < O(n log n) > > pour < < n ≤ 1000 > > .
** Mémoire**: `O(n)` pour la carte + `O(n)` pour le tableau de mots.

---

10. Le référencement et le choix de carrière

Mots clés
- Le code de chaîne le plus long
- LeetCode de programmation dynamique 1048
- Solution de Leetcode de Java
- Python Leetcode 1048
- C++ Leetcode 1048
- Question de l'interview du PDD
- Entretien avec l'ingénieur logiciel prép

Pourquoi les recruteurs aiment ce problème

Compétences Comment le problème le démontre
- C'est quoi ?
**Programmation dynamique**=PDD classique sur les séquences; vous montrez la compréhension de la définition de l'état et de la récurrence. Autres
Le tri par longueur est une étape propre et gourmande qui simplifie le DP. Autres
**Hashing**=L'efficacité de la recherche O(1) pour les vérifications antérieures. Autres
**Temps-Espace Échanges**Vous discutez de la raison pour laquelle la solution choisie est optimale par rapport à la force brute. Autres
**Clean Code** Autres

C'est vrai. Comment le cadrer sur LinkedIn ou le reprendre

> *La chaîne la plus longue (LeetCode #1048) – solution O(n log n) DP utilisant le tri avide et les cartes de hachage. Réduction de la complexité de O(n2) à O(n log n). Implémenté en Java, Python et C++. *

---

11. Références et lecture supplémentaire

1. Problème de LeetCode 1048 – https://leetcode.com/problèmes/longest-string-chain/
2. Voir la vidéo Comment nous pensons à une solution – 1 minute de vidéo.
3. Messages de blog DP & Top-Down Memoization – pour une théorie plus profonde.
4. TopCoder - Chaîne la plus longue – modèle DP similaire.

---

La pensée finale

Le problème **La chaîne la plus longue** est un exemple classique de transformation d'une question apparemment lourde de graphs en un DP propre avec une observation intelligente : *la longueur des mots conduit la chaîne*. Maître ce modèle et vous serez prêt pour un large éventail de questions d'entrevue qui testent DP, hachage, et raisonnement algorithmique. Bonne chance pour votre prochain entretien de codage ! C'est ce qu'il a dit