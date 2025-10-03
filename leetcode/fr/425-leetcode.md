---
titre: LeetCode 425. Mots carrés - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. La solution – 3 langues en une

Vous trouverez ci-dessous une implémentation prête à coller de **LeetCode 425 – Word Squares** dans **Java, Python et C++**.
Les trois solutions utilisent la même idée :
* **Backtracking** – nous construisons la rangée carrée par rangée.
* **La recherche rapide de préfixe** – une carte (`préfixe → liste de mots`) ou une petite trie nous donne tous les candidats qui correspondent au préfixe suivant dans le temps amorti O(1).

> **Pourquoi 3 langues? **
> * Java – souvent la langue de choix dans les interviews big-tech.
> * Python – le moyen le plus rapide de prototyper et de discuter de logique.
> * C++ – le langage le plus performant dans la programmation compétitive.

---

#### 1.1 Java (Trie + Backtracking)

"Java
Importation de java.util.*;

classe TrieNode {
Carte <Character, TrieNode> enfant = nouveau HashMap<>();
Liste <Integer> mots = nouvelle liste de distribution<>();
}

solution de classe publique {
racine de TrieNode privée = nouveau TrieNode();
mot int privé Len;
les mots de chaîne privée;

liste publique<Liste<String>> motSquares(String[] mots) {
Ça. mots = mots;
ce.wordLen = mots[0].longueur();
buildTrie(mots);

Liste <Liste<String>> res = nouvelle liste <>();
pour (Pièce w : mots) {
Liste <String> cur = nouvelle liste <>();
c.add(w);
backtrack(1, cur, res);
}
retour rés;
}

private vide backtrack(int step, List<String> cur, List<List<String>> res) {
si (étape == wordLen) {
res.add(new ArrayList<>(cur));
retour;
}
StringBuilder sb = nouveau StringBuilder();
pour (ligne de clôture : cur) sb.append(row.charAt(step));

pour (int idx : getWordsWithPrefix(sb.toString())) {
cur.add(mots[idx]);
backtrack(étape + 1, cur, res);
cur.remove(cur.size() - 1);
}
}

privé vide buildTrie(String[] mots) {
pour (int i = 0; i < mots. longueur; ++i) {
TrieNode noeud = racine;
pour (charc : mots[i].àCharArray()) {
noeud = noeud.child.computeIfAbsent(c, k -> nouveau TrieNode());
node.words.add(i);
}
}
}

liste privée<integer> getWordsWithPrefix(préfixe de la chaîne) {
TrieNode noeud = racine;
pour [charc : préfix.àCharArray()) {
noeud = noeud.child.get(c);
si (node == null) retourner Collections.videList();
}
noeud de retour. les mots;
}
}
«» "

> **Complexité** –
> *Time*: "O(N · 3^L)" dans le pire des cas (chaque préfixe a 3 options).
> *Espace*: `O(N · L)` pour la pile de tri et de récursion.

---

#### 1.2 Python (Dictionnaire des Préfixes + Backtracking)

'`python
Solution de classe:
def wordSquares(self, mots: List[str]) -> Liste[Liste[str]]:
si ce n'est pas des mots : retourner []

L = len(mots[0])
pref_map = {"" : mots}
pour w en mots:
pour i dans la plage (1, L+1):
pref_map.setdefault(w[:i], []).append(w)

res = []
def backtrack(step, cur):
si étape == L:
res.append(cur[:])
retour
préfixe = "".join(word[step] for word in cur)
pour le candidat dans pref_map.get(préfix, []):
cur.append(candidat)
retour (étape + 1, cur)
C. pop()

pour w en mots:
retour (1, [w])
retour res
«» "

> L'astuce du dictionnaire élimine le besoin d'un tri explicite et maintient le code très concis.

---

*## 1.3 C++ (Carte non ordonnée des préfixes + DFS)

'`cpp
solution de classe {
public:
vector<vector<string>> wordSquares(vector<string>& words) {
int L = mots[0].size();
non ordonné_map<string, vector<int>> Le présent règlement est obligatoire dans tous ses éléments et directement applicable dans tout État membre.
pour (int i = 0; i < words.size(); ++i) {
b) Préf[""].push_back(i);
pour (int k = 1; k <= L; ++k)
les mots [i].substr(0, k)].push_back(i);
}

vecteur<vecteur<chaîne>> rés;
vecteur <int> cur;
fonction <vit(int)> dfs = [&](int step) {
si (étape == L) {
vecteur <string> carré;
pour (int idx : cur) carré.push_back(words[idx]);
res.push_back(square);
retour;
}
préfixe de chaîne;
pour (int idx : cur) prefix.push_back(words[idx][step]);

pour (int next : pref[prefix]) {
cur.push_back(suivant);
dfs(étape + 1);
cur.pop_back();
}
};

pour (int i = 0; i < words.size(); ++i) {
cur.push_back(i);
dfs(1);
cur.pop_back();
}
retour rés;
}
};
«» "

> Remarquez comment la même logique est exprimée avec C++=s `std::function` et `unordered_map`.

---

- Oui. 2. Article de blog – Mot Places: les bons, les mauvais et les mauvais

> ** Mots-clés de référence:** Word Squares, LeetCode 425, Backtracking, Trie, Prefix Map, Codage Interview, Algorithm Design, Java, Python, C++, Job Interview, Technical Interview

---

2.1 Introduction

Word Squares est un puzzle trompeur qui est devenu un point de départ dans les questions d'entrevue algorithmiques. L'objectif est d'organiser un ensemble de mots de longueur égale dans une grille carrée de sorte que la ligne `k`‐th égale la colonne `k`‐th pour tous `k`. Il s'agit d'un excellent test de votre capacité à combiner **backtracking**, **prefix search** et **data structure design** – des compétences que les recruteurs dans les rôles d'ingénierie logicielle attribuent fortement.

---

2.2 Réévaluation des problèmes (Ce que vous devez savoir)

- **Input:** Un tableau `words` de chaînes uniques minuscules, toutes de la même longueur `L`.
- **Output:** Tous les carrés de mots possibles* qui peuvent être formés à partir de mots. Un mot peut être réutilisé plusieurs fois.
- **Contraintes:** "1 ≤ longueur de mots ≤ 1000", "1 ≤ L ≤ 4".

> **Pourquoi `L ≤ 4` importe**
> Une petite longueur de mot réduit considérablement l'espace de recherche, mais l'algorithme doit encore s'étendre à 1000 mots.

---

2.3 Le bien – propre, rapide et évolutif

Pourquoi il est bon
C'est quoi ?
Autres **Trie + Backtracking**= Recherche rapide de préfixe O(1). Les nœuds trient des indices de mots, donc la mémoire reste linéaire. Autres
**Préfixer la carte (Python/C++)** Autres
Chaque niveau de récursion construit la rangée suivante, éliminant le besoin d'un état compliqué. Autres
**Mots réutilisables** Parce que nous stockons des indices, un mot peut être inséré plusieurs fois sans duplication. Autres

**Traitement de la clé :** Un trie (ou une carte de hachage des préfixes) maintient l'arbre de retour taillé dans seulement des branches viables. C'est l'optimisation centrale qui transforme une force brute exponentielle en une solution pratique.

---

### 2.4 L'Ingénierie – Surveillante ou sous-optimisée

Pourquoi c'est mal
- C'est quoi ?
**Génération de la force brute**= Générer toutes les permutations de "mots" de longueur `L` puis filtrer.= O((N^L) · L^2) – impossible pour N=1000. Autres
Autres Pour chaque préfixe, scannez tous les mots. O(N · L) par récursion → O(N^L) cas le plus défavorable. Autres
Autres **Copier des carrés entiers**=Dupliquer le carré entier à chaque étape de la récursion.==Curn mémoire O(L2). Autres
Utiliser la profondeur de récursion > 1000 (p. ex. pour des mots plus longs). - Risque de débordement. Autres

> **Leçon:** Même une solution backtracking "Simple" peut devenir un *mauvais* si vous ignorez la recherche rapide de préfixe. La première étape pour éviter cela est de construire un *prefix index*.

---

### 2.5 Le "Ugly" – trop compliqué et difficile à maintenir

Pourquoi ça fait mal ?
C'est quoi ?
**Trues multiples et cartes**=True séparée pour chaque position du personnage + carte globale. Doublon du code; plus difficile à lire. Autres
**Mixing Languages**= Java utilise une classe complète, Python utilise une fonction, C++ utilise une lambda avec un état global. Rendre la comparaison entre langues douloureuse. Autres
**Constantes codées à l'aide d'un code ard**= `pour (int i = 0; i < words.size(); ++i)` boucles intérieures avec nombres magiques. Le principe des viols DRY. Autres
**Les variables mondiales inutiles**=Enregistrez tout comme des membres statiques. C'est difficile de tester l'unité. Autres

> **Fix:** S'en tenir à une seule structure de données par algorithme (soit *Trie* ou *Prefix Map*) et conserver la logique de récursion en un seul endroit. Une séparation claire des préoccupations est essentielle pour la lisibilité.

---

2.6 Analyse de la complexité – Ce que les recruteurs prennent en compte

1. **Heure**
* Construire le préfixe carte / trie: `O(N · L)`
* DFS / DFS avec taille: `O(N · 3^L)` ( pire-cas) – le facteur 3 provient de chaque préfixe ayant au plus 3 mots correspondants pour `L = 4`.
* L'exécution finale est dominée par le nombre de carrés *valides*.

2. **Espace**
* Trie ou carte: `O(N · L)`
* Pile de récursion: `O(L)`
* Stockage des résultats: `O(K · L2)` où `K` est le nombre de carrés valides.

---

2.7 Conseils pratiques pour l'entrevue

1. **Expliquer votre processus de pensée** – Commencez par décrire l'arborescence de récursion, puis montrez comment vous l'imprègnez avec une carte de trie ou de préfixe.
2. **Afficher le code, puis discuter des cas d'Edge** – par exemple, et si le préfixe n'est pas trouvé? – retourner une liste vide.
3. **Talk About Reusability** – Mettre en évidence que nous stockons des indices, pas des copies.
4. **Mention Complexity Early** – Parce que L ≤ 4, un trie maintient cette efficacité même avec 1000 mots. (en milliers de dollars)
5. **Offre Alternatives** – Si vous préférez Python, un simple dict de préfixes est plus propre; si la vitesse est primordiale, un trie vous donne un facteur plus serré et constant. (en milliers de dollars)

---

2.8 Comment cela vous prépare à une entrevue d'emploi

- **Conception de l'algorithme:** Vous démontrerez comment réduire un problème complet NP à quelque chose d'exécutable en quelques secondes.
- **Structures de données:** Les recruteurs aiment vous voir choisir le bon outil (hash-map vs. trie).
- ** Style de codage :** Code propre, noms de variables appropriés, et copie minimale montrent la maturité professionnelle.
- **Communication:** Marcher à travers les modèles Good/Bad/Ugly dans une entrevue montre que vous pouvez critiquer votre propre code, une compétence douce précieuse.

---

2.9 Mot final – du code à la carrière

Word Squares est plus qu'un puzzle ; c'est un microcosme de ce que les gestionnaires d'embauche veulent : ** utilisation des structures de données, récursion efficace et communication claire**.
- **Pratique** avec les extraits Java, Python et C++ ci-dessus.
- **Donnez vos propres tests** – par exemple, "mots = ["area", "lead", "wall", "lady", "ball"]".
- ** Expliquez l'algorithme** à un ami ou dans une interview simulée; l'enseignement est le meilleur moyen de cimenter la connaissance.

Lorsque vous atterrissez cette entrevue, apportez cette question (et le code) à la table. L'intervieweur appréciera que vous soyez prêt à écrire un code propre et efficace sur place, une compétence qui se traduit directement par la production de logiciels de qualité.

> * Bonne chance pour votre prochaine interview!*

---

- Oui. 3. Liste de contrôle rapide avant de soumettre

Liste de contrôle
C'est pas vrai.
Java (en anglais seulement) "root.child.computeIfAbsent()" reste serré. "Nouvel ArrayList<>(cur)" copie seulement le résultat final. Autres
Utiliser `defaultdict(list)` pour les préfixes. Autres
"unordered_map<string, vector<int>>` donne une recherche O(1). "std: fonction<evit(int)>" Garde la récursion en ordre. Autres

Copiez-collez l'extrait correspondant dans votre éditeur LeetCode/CodeSignal/InterviewBuddy et appuyez sur **Run**. Tous les trois devraient produire la même liste de carrés de mots pour toute entrée valide.

Bon codage – et bonne chance pour votre prochain entretien technique!