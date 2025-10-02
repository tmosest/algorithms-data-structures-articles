---
titre: LeetCode 336. Palindrome Paires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Les paires de palindromes – LeetCode 336
### Le dur problème, la meilleure solution et pourquoi cela compte dans les entrevues

> *Pairs de Palindrome, LeetCode 336, problème d'entretien dur, solution O(N), Java, Python, C++, Trie, palindrome détection

---

### TL;DR

* **Objectif** – Trouver toutes les paires d'index `(i, j)` de telle sorte que `words[i] + words[j]` est un palindrome.
* **Constraints** – "1 ≤ words.longueur ≤ 5 000", chaque mot pouvant atteindre 300 caractères.
* **Complexité requise** – "O(longueur totale de tous les mots)" (-)
* **Approche optimale** – Construisez un **Trie de mots inversés** et conservez une liste d'ID de mots qui peuvent former un palindrome avec le préfixe restant.
* **Langues** – Implémentation dans **Java, Python et C++**.

Vous trouverez ci-dessous le code complet pour chaque langue, suivi d'un article de blog détaillé qui passe par l'algorithme, ses compromis et la façon dont il met en valeur votre structure de données dans une entrevue d'embauche.

---

- Oui. 1. Mise en œuvre de Java

"Java
Importation de java.util.*;

***
* LeetCode 336 – Paires de palindrome
* Temps de runtime: O(-)word, Mémoire: O(-)word, alphabet
*/
solution de classe publique {

*** Trie noeud tenant l'index du mot se terminant ici et
* une liste d'indices dont le suffixe forme un palindrome
* reste du mot. */
classe statique privée TrieNode {
int wordIndex = -1; // -1 → aucun mot ne se termine ici
Carte<Caractère, TrieNode> suivante = nouveau HashMap<>();
Liste <Integer> palindromeSuffix = nouvelle liste d'array<>();
}

*** Vérifiez si la sous-chaîne s[i ... fin] est palindrome. */
booléen privé estPalindrome(String s, int i) {
int l = i, r = s.longueur() - 1;
pendant que (l < r) {
si (s.charAt(l) != s.charAt(r)) retourne faux;
l++; r--;
}
retour vrai;
}

liste publique<Liste<Intégrée>> palindromePairs(mots en attente[]) {
TrieNode root = nouveau TrieNode();

- Oui. Construisez le tri du mot inversé ---------- */
pour (int id = 0; id < words.longueur; id++) {
Chaîne w = mots[id];
Chaîne rev = nouvelle chaîneBuilder(w).reverse().toString();
TrieNode noeud = racine;

pour (int j = 0; j < rev.longueur(); J++) {
/* Si le suffixe de rev restant est un palindrome,
* puis le préfixe original de w peut être jumelé avec n'importe quel
* mot qui se termine dans ce nœud. Marque d'enregistrement. */
si (isPalindrome(rev, j))
node.palindromeSuffix.add(id);

c = rev.charAt(j);
noeud = noeud.next.computeIfAbsent(c, k -> nouveau TrieNode());
}
noeud.wordIndex = id; // marque la fin d'un mot
}

- Oui. Trouver toutes les paires de palindromes
Liste <Liste<entier>> résultat = nouvelle liste <>();

pour (int id = 0; id < words.longueur; id++) {
Chaîne w = mots[id];
TrieNode noeud = racine;

pour (int j = 0; j < w.longueur(); J++) {
/* Cas 3 : le nœud actuel termine un mot et le reste
* de w est palindrome → (id, node.wordIndex) */
si (node.wordIndex != -1 && noeud.wordIndex != id &&
estPalindrome(w, j))
résultat.add(Arrays.asList(id, node.wordIndex));

/* Déplacez la trie */
noeud = noeud.next.get(w.charAt(j));
si (noeud == nul) rupture;
}
si (noeud == null) continuer;

/* Cas 1 : correspondance complète (le mot se termine ici) */
si (node.wordIndex != -1 && node.wordIndex != id)
résultat.add(Arrays.asList(id, node.wordIndex));

/* Case 2: mots qui ont un suffixe palindrome avec le reste
* de w (entreposé pendant la construction de trie). */
pour (int other : node.palindromeSuffix)
result.add(Arrays.asList(id, autre));
}

le résultat du retour;
}
}
«» "

> **Pourquoi c'est une bonne réponse à l'entrevue* *
> 1. **Time‐optimal** – nous scannons chaque personnage au plus deux fois.
> 2. **Space-optimal** – les magasins trie n'ont besoin que des bords.
> 3. **Readability** – séparation claire des phases de construction et de recherche.

---

- Oui. 2. Mise en œuvre du Python (O(==word=))

'`python
de taper l'importation Liste, numéro

Classe TrieNode:
__slots__ = ('idx', 'enfants', 'pal_suffix')

def _init_(self):
Self.idx = -1 # -1 → aucun mot ne se termine ici
Enfants: Dict[str, 'TrieNode'] = {}
self.pal_suffix: List[int] = [] # word indices dont le suffixe est palindrome

Solution de classe:
def is_pal(self, s: str, start: int) -> C'est vrai.
retourner s[start:] == s[démarrer:]:

def palindrome Pairs(self, mots: List[str]) -> List[List[int]]:
racine = TrieNode()

C'est... Construire un tri de mots inversés ----------
pour i, w en énumération(mots):
rev = w[:-1]
noeud = racine
pour j, ch dans l'énumération (rev):
si self.is_pal(rev, j):
node.pal_suffix.append(i)
noeud = noeud.children.setdefault(ch, TrieNode())
noeud.idx = i

C'est... Trouver des paires de palindromes - Oui.
res = []

pour i, w en énumération(mots):
noeud = racine
pour j, ch dans l'énumération(w):
# Affaire 3
si node.idx != -1 et node.idx != i et self.is_pal(w, j):
res.append([i, node.idx])
noeud = noeud.children.get(ch)
si ce n'est pas le nœud:
pause
Sinon:
# Le noeud n'est pas Aucun
Cas 1
si node.idx != -1 et node.idx != i:
res.append([i, node.idx])
Deuxième affaire
pour les autres dans node.pal_suffix:
res.append([i, autre])

retour res
«» "

> **Notes spécifiques au python**
> * Utilisez `_slots__` pour réduire les frais de mémoire des nœuds triés.
> * L'aide `is_pal` est appelée seulement quelques fois par mot.

---

- Oui. 3. Mise en œuvre C++

'`cpp
#incluez <vecteur>
#incluez <string>
#inclut <non-ordonné_map>

utilisant l'espace de noms std;

classe TrieNode {
public:
int wordIdx = -1; // -1 → aucun mot ne se termine ici
une_carte non ordonnée<char, TrieNode*> enfant;
vector<int> palSuffix; // indices de mots dont le suffixe est palindrome

~TrieNode() {
pour (auto &p : enfant) supprimer p.seconde;
}
};

solution de classe {
// helper: vérifier si s[pos .. fin] est palindrome
bool isPal(chaîne de caractères &s, int pos) {
pour (int l = pos, r = (int)s.size() - 1; l < r; ++l, --r)
si (s[l] != s[r]) retourne faux;
retour vrai;
}

public:
vector<vector<int>> palindromePairs(vector<string> &words) {
TrieNode *root = nouveau TrieNode();

- Oui. Construire un tri de mots inversés ---------- */
pour (int id = 0; id < (int)words.size(); ++id) {
const string &w = words[id];
chaîne rev = chaîne(w.rbegin(), w.rend());
TrieNode *node = racine;

pour (int j = 0; j < (int)rev.size(); ++j) {
si (estPal(rev, j))
node->palSuffix.push_back(id);
char c = rev[j];
si (!node->child.count(c))
node->child[c] = nouveau TrieNode();
noeud = noeud->enfant[c];
}
node->wordIdx = id;
}

- Oui. Trouver des paires de palindromes
vecteur<vecteur<int>> ans;
pour (int id = 0; id < (int)words.size(); ++id) {
const string &w = words[id];
TrieNode *node = racine;
pour (int j = 0; j < (int)w.size(); ++j) {
// Affaire 3
si (noeud->wordIdx != -1 && noeud->wordIdx != id &&
estPal(w, j))
as.push_back({id, noeud->wordIdx});

c = w[j];
si (!node->child.count(c)) pause;
noeud = noeud->enfant[c];
}
si (!node) continue;

// Cas 1
si (node->wordIdx != -1 && node->wordIdx != id)
as.push_back({id, noeud->wordIdx});

// Affaire 2
pour (int other : node->palSuffix)
as.push_back({id, autre});
}

supprimer root; // destructeur de TrieNode libérera les enfants
le retour des an;
}
};
«» "

> ** Remarques spécifiques au C++**
> * `unordered_map` donne une recherche moyenne de bord O(1).
> * Explicite `delete root;` nettoie les nœuds triés attribués.

---

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais des paires de Palindrome

#### 4.1 Les bonnes: Pourquoi l'idée de trie gagne

1. ** Scan linéaire** – Chaque caractère de chaque mot est visité un nombre constant de fois (une fois en insérant, une fois en interrogeant).
2. **Pas de collisions avec le hash** – La trie est déterministe; chaque chemin représente un suffixe d'un mot inversé.
3. **Création d'un palindrome** – En enregistrant *suffixes palindromiques* lors de la construction, nous évitons de repiquer les mêmes sous-chaînes pendant la recherche.
4. **Extensible** – La même structure peut être réutilisée pour les problèmes *anagrammes*, *préfixe-suffixe* ou *reverse-lookup*.
5. **Interrogateur-Amis** – Ça montre que vous comprenez :
* Trie construction
* Détection du palindrome en O(longueur)
* Échanges espace/temps

> **Takeaway d'entrevues clés** – J'ai construit une structure de données qui me permet de répondre à *toute* requête palindrome-concaténation en temps linéaire. (en milliers de dollars)

---

### 4.2 La mauvaise: les cas de bord et l'empreinte de mémoire

Pourquoi ça va ?
- C'est quoi ?
**La corde empty est un palindrome. Utiliser explicitement """ comme cas séparé ou stocker son index dans le tri. Autres
**Le problème garantit que tous les mots sont uniques, mais les données du monde réel ne le sont peut-être pas. Dupliquer avant de construire, ou stocker plusieurs indices si des duplicatas sont autorisés. Autres
**Grand alphabet** Un tri avec un énorme alphabet (par exemple Unicode) pourrait souffler la mémoire. Restriction à ASCII/UTF‐8 pour les contraintes de LeetCode. Autres
Chaque noeud stocke un `HashMap` / `unordered_map`. Avec 5 000 mots × 300 caractères, dans le pire des cas ~1,5 million de nœuds. Autres

---

### 4.3 Le lamentable: Pièges communs et comment les éviter

Pièges Type de bug
- C'est quoi ?
**Null-pointer lors de la recherche** Utilisez un garde (`si (!node) break;`) et une clause `else` après la boucle dans C++/Java, ou `break` & `continue` logique dans Python. Autres
**Solf-pairing**=Jouer un mot avec lui-même ('i == j') quand le mot est un palindrome. Cochez explicitement `node.idx != id`. Autres
**Vérification du palindrome incorrecte** , en utilisant `s[start:] == s[:-1]` qui inverse la chaîne *toute* chaque appel. Autres Cochez seulement la sous-chaîne `s[start:]` contre son inverse. Autres
**Dupliquer les résultats**. Soit dédoubler la liste de résultats avec un "set", soit concevoir l'algorithme de sorte que chaque paire ne soit ajoutée qu'une seule fois (comme indiqué). Autres

---

- Oui. 5. SEO–Friendly Wrap‐Up – Un terrain qui travaille

> **Méta-description** – Découvrez la solution Trie linéaire pour LeetCode 336 – Palindrome Pairs, avec le code Java, Python et C++, ainsi qu'un article prêt à l'interview qui vous montre que vous êtes un assistant de structure de données. (en milliers de dollars)

1. **Afficher l'algorithme** – Les extraits de code ci-dessus sont prêts à copier, ils impressionneront un gestionnaire d'embauche qui vérifie votre soumission par rapport à la suite de test LeetCode.
2. **Ajouter un message LinkedIn** – Poster une courte écriture de la solution avec un lien vers votre repo GitHub; utiliser des balises comme `#Leetcode336 #PalindromePairs #DataStructures #Java #Python #C++ #InterviewPrep'.
3. **Construire une page de portfolio** – Organisez l'article du blog sur Medium ou votre site personnel avec le titre *=Palindrome Pairs – LeetCode 336 (Java/Python/C++)* et intégrez les blocs de code.
4. **Exposer les compromis** – Dans une entrevue en direct, soyez prêt à discuter *temps vs espace*, de l'importance de manipuler la chaîne vide, et de la façon dont la solution s'écrase vers des alphabets plus grands.

---

- Oui. 6. Prise Liste de contrôle pour l'entrevue

Pourquoi ça aide ?
C'est quoi ?
Expliquez d'abord le concept de *Trie de mots inversés*. Définit le contexte rapidement. Autres
Description des trois cas (comparaison complète, préfixe palindrome, suffixe palindrome). Démontre la résolution systématique des problèmes. Autres
"["bat", "tab", "cat"]". Autres
Mentionnez la manipulation de l'étui (""", duplicata). Montre la robustesse. Autres
Mettre en avant la garantie "O(longueur totale)". LeetCode doit être complexe. Autres
Gardez le code propre, commenté et divisé en phases *build* + *search*. Autres

---

- Oui. 7. Pensée finale

Maîtriser *Pairs de Palindrome* prouve que vous pouvez jongler ** manipulation de cordes**, ** logique de palindrome** et **conception efficace de la structure des données**—tous les sujets essentiels des entrevues de codage de niveau supérieur. Les solutions Java, Python et C++ ci-dessus sont prêtes à passer, linéaires et prêtes à impressionner les recruteurs à la recherche d'un arrière-plan algorithmique fort.

Bon codage, et bonne chance d'atterrir ce prochain rôle d'ingénierie de logiciels!