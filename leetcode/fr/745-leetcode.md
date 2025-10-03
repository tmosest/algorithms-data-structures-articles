---
titre: LeetCode 745. Recherche préfixe et suffixe -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 745 – **Préfixe et suffixe de recherche**
> **Objectif:** Trouvez l'index d'un mot qui commence par un préfixe donné **et** se termine par un suffixe donné.
> **Langues:** Java.
> **Pourquoi ça compte :** Ce problème est une question d'entrevue courante qui teste la connaissance des essais, la manipulation des chaînes et le prétraitement pour les requêtes rapides. Résoudre bien peut vous poser un emploi à Google, Amazon, Microsoft, ou n'importe quelle entreprise de haute technologie.

---

Aperçu du problème

Description
C'est pas vrai.
**Nom**
Difficulté
**Input**="WordFilter(words)` – tableau de chaînes (1 ≤ `words.length` ≤ 104, chacune 1 ≤ `words[i].length` ≤ 7) <br>`f(pref, suff)` – deux chaînes (1 ≤ `pref.length, suff.length` ≤ 7)
**Extrait**= Indice (0-basé) du mot **dernier** qui commence par "pref" et se termine par "suff". Retour **-1** si ce mot n'existe pas. Autres
Jusqu'à 104 appels à "f". Toutes les chaînes ne contiennent que des lettres anglaises minuscules. Autres

> **Exemple**
> ```texte
> WordFilter wordFilter = nouveau WordFilter(["Apple"]);
> motFilter.f("a", "e"); // → 0
> `` "

---

Une idée fondamentale

Le défi consiste à répondre rapidement à de nombreuses questions.
Un balayage linéaire naïf (« O(N) » par requête) est trop lent.
**Pré-traitement** les mots avec une structure de données qui supporte *préfixe* et *suffixe* dans **O(1)** ou **O(L)** le temps (où *L* ≤ 7) est la clé.

Double trie (préfixe + suffixe)
Construisez deux essais :

1. **Prefix trie** – stocke tous les préfixes de chaque mot.
2. **Suffix trie** – stocke tous les suffixes inversés de chaque mot.

Au cours d'une requête, marchez tous les deux en parallèle pour rassembler les mots des candidats, puis entrecroisez les deux ensembles de résultats et retournez l'index le plus élevé.

**Pour**
* Simple à comprendre.
* Fonctionne bien quand la longueur des mots est minuscule (- 7).

**Cons**
* Nécessite deux essais séparés.
* Les ensembles d'interconnexion pour chaque requête peuvent être coûteux lorsque de nombreux mots partagent le même préfixe/suffixe.

### Trie unique avec séparateur (LeetCode-Recommandé)
Insérer pour chaque mot *w* toutes les chaînes du formulaire
`suffix + '{' + w` (où `{` est un caractère lexicographiquement plus grand que ‘z').
Lors d'une requête, construire la clé `suff + '{' + pref` et rechercher la trie.

**Pour**
* Seulement **un** trie.
* Chaque noeud stocke l'indice **maximum** (poids) de n'importe quel mot qui passe à travers lui → réponse est directement le noeud poids.
* Des requêtes extrêmement rapides (« O(L) »).

**Cons**
* Logique d'insertion légèrement plus complexe.
* Utilise 27 pointeurs par noeud (26 lettres + séparateur).

Le blog ci-dessous se concentre sur la solution **single-trie** car elle est la plus efficace et largement utilisée dans les entrevues.

---

Algorithme Marcher

1. **Pré-processus**
Pour chaque mot `w` à l'index `i`:
* Pour chaque suffixe `s` de `w` (y compris le suffixe vide):
* Insérez la chaîne `s + '{' + w` dans la trie.
* Lors de l'insertion, mettre à jour le "poids" de chaque nœud traversé à "i".
* Insérer `"{" + w` pour gérer le cas d'un suffixe vide.

2. **Query** "f(pref, suff)"
* Construisez la clé de recherche: `key = suff + '{' + pref`.
* Marchez le trie suivant `key`.
* Si à n'importe quel point le chemin casse → retour **-1**.
* Sinon → retourner le `poids` stocké au dernier nœud.

Parce que nous conservons toujours le poids **dernier** (le plus grand indice), la valeur retournée est exactement ce que le problème demande.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
(N = 104, L ≤ 7) – mais dans la pratique ~105–106 opérations. Autres
**Query** (`f`)" "O(L)" (14 char traversals). Autres

> Avec ces mots courts, les constantes sont négligeables, donnant **sous-milliseconde** par requête sur les machines réelles.

---

Cas de bord

Autres Décision Comment on s'en occupe
-- -- -- -- -- -- --
Ajouter ""{" + w` (c.-à-d., suffixe vide + séparateur + mot). Autres
La clé de requête est `suff + '{''. Autres
Autres Aucun mot correspondant.La traversée frappera un noeud manquant → retour **-1**. Autres

---

Mise en œuvre

Voici des implémentations propres et prêtes à la production pour **Java**, **Python** et **C++**.

> **Astuce :** Lors de l'affichage de votre code dans une entrevue ou sur votre GitHub, ajoutez des commentaires qui indiquent clairement le but de chaque partie (surtout la logique du séparateur).

---

Mise en œuvre Java (Essai unique +

"Java
// Java 17
classe WordFilter {
int privée statique ALPHABET_SIZE = 27; // 26 lettres + ' { '

classe statique privée TrieNode {
TrieNode[] suivante = nouveau TrieNode[ALPHABET_SIZE];
poids int = -1; // indice max passant par ce nœud
}

racine de TrieNode finale privée = nouveau TrieNode();

Int privé charIndex(char c) {
retour c == « { » ? 26 : c - « a »;
}

insert de vide privé(clé de maintien, poids int) {
TrieNode noeud = racine;
pour (char ch : key.toCharArray()) {
idx = charIndex(ch);
si (node.next[idx] == null) {
node.next[idx] = nouveau TrieNode();
}
noeud = noeud.next[idx];
poids = poids; // conserver l'indice le plus récent
}
}

wordFilter(String[] mots) {
pour (int i = 0; i < words.longueur; i++) {
Chaîne w = mots[i];
// Tous les suffixes de w
pour (int start = 0; start < w.length(); start++) {
insérer(w.substring(start) + "{" + w, i);
}
// Le suffixe vide (cas de bord)
insérer("{" + w, i);
}
}

Int public f(String pref, String suff) {
Clé de chaîne = suff + "{" + pref;
TrieNode noeud = racine;
pour (char ch : key.toCharArray()) {
idx = charIndex(ch);
si (node.next[idx] == null) retourne -1;
noeud = noeud.next[idx];
}
noeud de retour. poids;
}
}
«» "

---

Mise en œuvre du Python (Tri simple + -)

'`python
# Python 3.9+

Classe TrieNode:
__slots__ = ('suivant', 'poids')
def _init_(self):
Self.next = [Aucune] * 27 # 26 lettres + '{ '
poids propre = -1


cours WordFilter:
def __init_(self, mots):
Self.root = TrieNode()
pour le poids, mot en énumération(mots):
Tous les suffixes de mots
pour i dans la plage(len(word)):
clé = mot[i:] + "{" + mot
_insérer(clé, poids)
Le suffixe vide
_insérer("{" + mot, poids)

def _insert(self, clé, poids):
noeud = self.root
pour ch en clé:
idx = 26 si ch == '{' autre ord(ch) - 97
si node.next[idx] est None:
node.next[idx] = TrieNode()
noeud = noeud.next[idx]
poids = poids

def f(self, pref, suff):
key = suffi + "{" + pref
noeud = self.root
pour ch en clé:
idx = 26 si ch == '{' autre ord(ch) - 97
si node.next[idx] est None:
retour -1
noeud = noeud.next[idx]
noeud de retour. Poids
«» "

---

Mise en œuvre de C++ (Tri simple + C)

'`cpp
// C++17
classe WordFilter {
public:
Numéro de structure {
poids int = -1;
std::array<Node*, 27> enfant = {nullptr};
};
Noeud* racine = nouveau Noeud();

insert vide(const std::string & key, poids int) {
Noeud* cur = racine;
pour(charc : clé) {
int idx = (c == « { ») ? 26 : c - « a »;
if(!cur->child[idx]) cur->child[idx] = nouveau nœud();
cur = cur->child[idx];
cur->weight = poids; // conserver l'indice le plus élevé
}
}

WordFilter(std::vector<std::string> mots) {
pour(int i = 0; i < (int)words.size(); ++i) {
const string& w = mots[i];
pour(int j = 0; j < (int)w.size(); ++j) {
insérer(w.substr(j) + "{" + w, i);
}
insert("{" + w, i); // cas de suffixe vide
}
}

int f(string pref, string suff) {
touche de chaîne = suff + "{" + pref;
Noeud* cur = racine;
pour(charc : clé) {
int idx = (c == « { ») ? 26 : c - « a »;
if(!cur->child[idx]) retourne -1;
cur = cur->child[idx];
}
poids de retour;
}
};
«» "

---

Cas d'essai

Texte
mots = ["application", "application", "application", "banane"]
requêtes =
f("app", "le") → 2 (applesauce)
f("ap", "ly") → 1 (appliquer)
f("ba", "na") → 3 (banane)
f("c", "d") → -1
«» "

Effectuez vos propres tests unitaires avec quelques milliers de mots aléatoires pour être absolument confiant.

---

Bien, mal, Méchant

#'''''''''''''''''''''
- C'est quoi ?
Le prétraitement "O(N·L2)" est trivial pour *L* = Aucun.
Autres Les nœuds "O(N·L2)" sont acceptables (~106). Aucun.
**Readability**Le code de double-tri est intuitif mais plus lent. Autres
Autres Plus facile à étendre avec d'autres requêtes de chaîne. Double-trie duplication de la logique.
Une sur-ingénierie (p. ex. en utilisant `unordered_map` par noeud) fera mal. Autres

> **À emporter :** Utilisez le tour de la série unique – c'est le plus rapide et celui que les intervieweurs attendent de vous.

---

Liste de contrôle sur l'approche à suivre (Job-Ready)

- [ ] . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
- [ ] Savoir pourquoi `{` est sûr comme séparateur.
- [ ] * Insérez * qui met à jour le poids du nœud.
- [ ] -Construisez la touche `suffix + '{' + préfixe ' dans les requêtes.
- [ ] -Poignez le suffixe vide en insérant ""{" + mot".
- [ ] - Discuter de la complexité: `O(N·L2)` build, `O(L)` requête.
- Montrer les tests unitaires.
- [ ] Soyez prêt à expliquer *bon* (vitesse), *mauvais* (complexité), *gros* (trick de codage).

---

Rubriques du blog

Voici un billet de blog complet que vous pouvez coller dans Medium, Dev.to, ou votre blog personnel. Il contient tous les mots-clés que les recruteurs recherchent.

---

# LeetCode 745 – Master Prefix & Suffix Rechercher en Java, Python & C++

> **Mots-clés**: LeetCode 745, Recherche préfixe et suffixe, WordFilter, trie, Java, Python, C++, interview, structures de données, OOP, défi de codage, interview ingénieur logiciel

- Oui. 1. Qu'est-ce que LeetCode 745?

LeetCode 745 vous défie de construire un **WordFilter** qui supporte les requêtes du formulaire:

Texte
f(préfixe, suffixe) → plus grand index d'un mot qui commence par préfixe et se termine par suffixe
«» "

C'est un problème de chaîne classique que chaque *entretien d'ingénieur logiciel* doit maîtriser.

- Oui. 2. Le piège du séparateur: Pourquoi `{` Travaux

Lorsque vous voyez `mot + "{" + suffixe` dans une solution, pensez à:

- **Aucune collision**: `{` n'est pas une lettre, donc elle ne peut pas apparaître dans les mots d'entrée.
- **Constante traversée**: chaque magasin `TrieNode` au plus 27 enfants (26 lettres + `{`).

- Oui. 3. Bâtir la trie - O(N·L2) Temps, rapide dans la pratique

Même si le temps de construction théorique est quadratique en longueur de mots, avec *L* ≤ 7 le temps réel est une poignée de millisecondes.

- Oui. Code Java

"Java
classe WordFilter { /* ... */ }
«» "

Code Python

'`python
classe WordFilter: /* ... */
«» "

C++ Code

'`cpp
classe WordFilter { /* ... */ };
«» "

- Oui. 4. Interrogation en temps O(L) – Réponses en sous-miliseconde

Toutes les requêtes impliquent la traversée au plus 14 nœuds (préfixe + suffixe ≤ 7 chacun). C'est pourquoi les solutions passent 104+ requêtes en < 0,01 s sur un ordinateur portable.

- Oui. 5. Cas de bord et conseils pratiques

- **Empty suffix** → insérer `"{" + mot`.
- **Le préfixe Empty** → touche est juste `suffix + "{"`.
- **Aucune correspondance** → retour `-1`.
- **Tests unitaires**: Vérifiez avec des milliers de mots aléatoires.

- Oui. 6. Secrets d'entrevue: Expliquez le bon, le mauvais et le mauvais

- **Bon**: Des questions rapides sur la foudre, des mises à jour sur le poids des nœuds propres.
- **Bad**: Sur-ingénierie avec des cartes de hachage par noeud.
- **Ugly**: Oublier de commenter la logique du séparateur.

- Oui. 7. Liste de contrôle des recrues

- Connaissance de la structure des données (tries).
- Efficacité algorithmique (construction O(N·L2), requête O(L).
- Nettoyez le code en Java, Python, C++.
- Essais unitaires complets.
- Capacité d'expliquer les compromis.

---

Mot final

Si vous ace LeetCode 745 avec l'implémentation **simple trie + .., vous montrez aux recruteurs que vous:

- Peut mettre en place des structures de données sophistiquées.
- Comprendre pourquoi certains trucs (comme le séparateur) sont nécessaires.
- Offrez un code rapide et durable.

Allez-y, postez le code sur GitHub, écrivez un blog et continuez à pratiquer ! C'est ce qu'il a dit.

---

Bon codage et bonne chance avec vos entrevues!