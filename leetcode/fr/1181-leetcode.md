---
titre: LeetCode 1181. Avant et après Puzzle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1181 – Avant et après Puzzle
### 3-Way Code & a - How-To-To Blog Post pour la prochaine entrevue

---

- Oui. 1. Récapitulation des problèmes

Avec une liste de phrases, construisez tous les puzzles possibles *Avant & Après* :

* Un puzzle est formé par la fusion **deux** phrases différentes.
* Seul le **dernier mot** de la première phrase et le **premier mot** de la deuxième phrase sont fusionnés (le mot lui-même n'apparaît qu'une seule fois).
* L'ordre des deux phrases est important – à la fois `i → j` et `j → i` doivent être considérés.
* La sortie est une liste **triée** de chaînes de puzzle **unique**.

> **Exemple**
> `["code d'écriture", "code rocks"]` → `"code d'écriture rocks"`

---

- Oui. 2. Stratégie de haut niveau

1. **Pré-processus** chaque phrase pour stocker son premier et dernier mot.
2. **Carte**:
* `firstWord → Liste<phrases qui commencent par ce mot> "
* `lastWord → Liste<phrases qui se terminent par ce mot> "
3. Pour chaque phrase `p` (comme la première)
* chercher toutes les phrases qui commencent par `p.last C'est écrit.
* Pour chaque match `q`, fusionner:
`p + " + q.substring(q.firstWord.longueur()+1)`
(laisser le mot dupliqué de `q`).
4. Insérez chaque résultat dans un `TreeSet` (automatically dedupes & tries).
5. Convertir l'ensemble en une liste et retourner.

C'est **O(n2)** dans le pire des cas, mais avec `n ≤ 100` il est trivial.
L'utilisation de la mémoire est `O(n)`.

---

- Oui. 3. Mise en œuvre du code

Vous trouverez ci-dessous des solutions prêtes à coller dans **Java, Python et C++**.
Tous suivent la même idée algorithmique et compiler avec la bibliothèque standard seulement.

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<String> avant etaprèsles phrases(String[]) {
// Cartes pour une recherche rapide
Carte<String, Liste<String>> PremièreWordMap = nouvelle HashMap<>();
Carte<String, Liste<String>> lastWordMap = nouvelle HashMap<>();

// Pré-processus de chaque phrase
pour (String p : phrases) {
Parties de chaînes = p.split(");
Chaîne d'abord = parties[0];
Chaîne dernière = parties[parties.longueur - 1];

firstWordMap.computeIfAbsent(first, k -> new ArrayList<>()).add(p);
LastWordMap.computeIfAbsent(dernier, k -> nouveau ArrayList<>()).add(p);
}

// Arbre Set donne la duplication + tri
Définir le résultat <String> = nouveau TreeSet<>();

pour (Principales phrases) {
Chaîne[] firstParts = firstPhrase.split(");
Chaîne lastWord = FirstParts[firstParts.longueur - 1];

Liste des candidats <String> = premierWordMap.getOrDefault(dernierWord, Collections.videList());
pour (DeuxièmePrintemps: candidats) {
si (firstPhrase.egals(secondPhrase)) continue; // i != j

Chaîne[] deuxièmeParties = deuxièmePhrase.split(");
// Supprimer le mot dupliqué
Chaîne fusionnée = première Phrase + " + "
Chaîne.join("", Arrays.copyOfRange(secondeparties, 1, deuxièmeparties.longueur));
résultat.add(fusionné);
}
}

retourner une nouvelle liste de distribution <>(résultats);
}
}
«» "

---

3.2 Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
avant EtAfterPuzzles(self, phrases: List[str]) -> List[str]:
first_map = defaultdict(list) # first mot -> phrases
last_map = defaultdict(list) # default word -> phrases

# Prétraitement
pour p en phrases:
mots = p.split()
premier_map[mots[0]].appendice(p)
last_map[words[-1]].append(p)

res = set()

pour p en phrases:
last_word = p.split() [-1]
pour q dans first_map.get(last_word, []):
Si p == q: # i != j
poursuivre
fusion = p + " + " .join(q.split()[1:])
res.add(fusionné)

retour trié(s)
«» "

---

#### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur <string> avantAndAfterPuzzles(vecteur<string>& phrases) {
unordered_map<string, vector<string>> premier, dernier;
résultat non ordonné_set<string>;

// Aide à la séparation
fractionnement automatique = [](chaîne &s Const) {
vecteur <string> les mots;
chaîne de caractères cur;
istringstream iss;
pendant que (iss >> cur) words.push_back(cur);
les mots de retour;
};

// Préprocessus
pour (const string &p : phrases) {
mots automatiques = split(p);
premier[mots.front()].push_back(p);
last[words.back()].push_back(p);
}

// Construire des puzzles
pour (const string &p : phrases) {
auto w = split(p);
const string &last Word = w.back();
auto it = first.find(lastWord);
si (it == first.end() continue;

pour (const string &q : it->second) {
si (p == q) continuer; // i != j
auto wq = split(q);
chaîne fusionnée = p;
pour (size_t i = 1; i < wq.size(); ++i) {
fusionné += " + wq[i];
}
result.insert(fusionné);
}
}

vector<string> ans(result.begin(), result.end());
tri(ans.begin(), ans.end());
le retour des an;
}
};
«» "

---

- Oui. 4. Blog Post: Avant et après Puzzle – LeetCode 1181: Le bon, le mauvais et le mauvais

---

#### Titre (Référencement ami)

*Cracking LeetCode 1181 – Avant et après Puzzle: Java/Python/C++ Solutions + Conseils d'entrevue

*Mots clés: LeetCode, Avant et Après Puzzle, prep interview, solution Java, solution Python, solution C++, algorithme, manipulation de chaînes, interview de codage, interview de programmation, problème algorithmique. *

---

Introduction

> Dans les interviews de codage, LeetCodeS *Avant et après Puzzle* (Problème 1181) est un défi de manipulation de chaînes de caractères qui est trompeur et qui teste votre capacité à penser aux limites de *mot*, *hash-mapping* et *déduplication*. Dans cet article, nous allons parcourir le problème, montrer des solutions propres en Java, Python et C++, et discuter d'écueils qui peuvent voyager jusqu'à des personnes interrogées aguerries. *

---

#### Résumé du problème

- **Input** – Array de "phrases" (chacune est une chaîne à espacement unique de lettres anglaises minuscules).
- **Objectif** – Pour chaque paire ordonnée `(i, j)` où `i φ j`, si le dernier mot de `phrases[i]` égale le premier mot de «phrases[j]», les fusionner en une seule phrase:
«» "
"phrase[i] phrase[j]" // mais laisser tomber le mot dupliqué
«» "
- **Output** – Toutes les phrases fusionnées distinctes, triées lexicographiquement.

---

Pourquoi est-ce bon pour les entrevues ?

1. ** Contraintes claires** – «n ≤ 100», «len ≤ 100». Parfait pour enseigner *force brute* vs *optimisation* pensée.
2. **Encourager Hashing** – L'idée principale est de faire correspondre les mots rapidement en utilisant des cartes de hachage.
3. **Manipulation de la chaîne** – Un bon test de la façon dont vous divisez, rejoignez et évitez les erreurs hors-par-un.

---

C'est vrai. Les pièges communs

Pourquoi ça arrive
- Oui.
**Utiliser des boucles imbriquées naïvement est très bien ici, mais beaucoup de candidats ajoutent une complexité inutile. Conservez O(n2) mais précalculez les cartes du premier/dernier mot pour éviter de les recouper. Autres
**Inclure l'auto-puzzle** ('i == j') Sauter explicitement lorsque les indices ou les chaînes correspondent. Autres
**Des mots dupliqués dans la fusion** Supprimer via `substring` ou `split[1:]`. Autres
**Pas de duplication**= Différentes paires peuvent produire la même chaîne fusionnée.= Utiliser un `Set` ou `TreeSet` avant de convertir en liste. Autres
**Wrong trie**= Retourner une liste non triée. Utiliser le tri intégré ou `TreeSet`. Autres

---

C'est vrai. Les cas de bord

1. **Expositions à mots simples** – « a » est à la fois le premier et le dernier mot.
2. **Dupliquer les phrases en entrée** – par exemple, "["ab ba", "ab ba"]".
3. **Plus grand nombre de duplicata** – un a a a= → beaucoup d'appariements mais un résultat unique.
4. **Très longues phrases** – jusqu'à 100 caractères ; évitez les opérations de chaînes de caractères O(longueur2).

---

Solution étape par étape

1. **Diffuser chaque phrase en mots** – `split("")`.
2. **Enregistrement** :
* `firstWordMap[first] → liste des phrases commençant par ce mot "
* `lastWordMap[last] → liste des phrases se terminant par ce mot "
(Les deux peuvent être `HashMap<String, List<String>>` dans Java, `defaultdict(list)` dans Python, ou `unordered_map<string, vector<string>>` dans C++.)
3. **Pour chaque phrase `p` comme première partie**:
* `dernier = p.dernier Mots "
* Pour chaque candidat `q` dans `firstWordMap[dernier]` (où `q!= p`):
* Fusionner: `p + " " + q.substring(q.firstWord.length() + 1)` (Java) ou similaire dans d ' autres langues.
4. **Insérer dans un "Set"** pour garantir l'unicité et l'ordre (un "TreeSet" ou un ensemble trié).
5. **Retour** la liste triée.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Pré-traitement Autres
"O(n2 * w)" (le pire cas, mais "n ≤ 100")
Tri de `O(k log k)` où `k` = nombre de résultats uniques Autres

Avec les contraintes données, c'est confortablement rapide.

---

#### Code Snippets (Prêt à l'entrevue)

*Java* – montré plus tôt.
*Python* – montré plus tôt.
*C++* – montré plus tôt.

> **Astuce:** Dans les interviews, vous pouvez d'abord montrer la double boucle de force brute (claire et correcte), puis optimiser par le hachage. Cela démontre à la fois la justesse et l'efficacité.

---

Les pensées finales

*Before & After Puzzle* est une **gold-mine** pour les intervieweurs : elle est courte, couvre les concepts essentiels, et laisse la place à un candidat pour parler des structures de données, de la gestion des cas de bord et du style de code.

**Conseils pratiques:**

1. Implémentez les trois solutions vous-même ; être couramment en Java, Python et C++ montre une polyvalence.
2. Exécutez votre code sur les entrées de l'échantillon (et certains cas de bord que vous créez).
3. Expliquez à haute voix la logique en écrivant le code: les intervieweurs aiment la clarté de la pensée.

Bonne chance, et que vos énigmes soient toujours agréables !

---

C'est vrai. À propos de l'auteur

> *[Votre nom]* est un ingénieur logiciel chevronné qui a aidé les équipes à gagner des entrevues de codage sur LeetCode. Suivez-moi pour plus d'algorithmes, de guides de préparation d'entrevues et de perspectives de carrière.

---

Joyeux codage – et heureux entretien!