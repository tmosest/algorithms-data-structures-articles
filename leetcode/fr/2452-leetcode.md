---
titre: LeetCode 2452. Mots dans deux éditions du dictionnaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2452 – Mots dans deux éditions du dictionnaire
*Brute-Force → Trie → Votre portfolio prêt à l'entrevue*

Ci-dessous vous trouverez **full, ready-to-paste code** dans **Java, Python et C++** pour deux approches:

Pourquoi ça compte dans les interviews
- C'est quoi ?
Brute-Force (O(Q·D·L))""O(m · n · L)""" "O(1)"" montre que vous pouvez résoudre le problème naïvement, bon pour un . Autres
Trie (O(L · D + Q · L))" "O(L · D + Q · L)"" "O(L · D)" Démontre une optimisation classique de la structure des données – un drapeau rouge pour les entrevues de codage. Autres

> **TL;DR** – Utilisez le trie si les contraintes augmentent (par exemple `L` jusqu`à 105). Pour l'ensemble de test 100 mots LeetCode, la force brute est plus que rapide.

---

## -Déclaration de problème (Code Leet 2452)

> On vous donne deux tableaux de chaînes, **`queries`** et **`dictionary`**.
> Tous les mots sont en minuscules et **la même longueur `L`**.
> Dans une édition, vous pouvez changer n'importe quelle lettre à toute autre lettre.
> Retourner tous les mots de « requêtes » qui peuvent devenir *quelques* mots de « dictionnaire » après au plus **deux modifications**.
> Préservez l'ordre original des requêtes.

*Contrôles*
«» "
1 ≤ requêtes.longueur, dictionnaire.longueur ≤ 100
1 ≤ L ≤ 100
«» "

---

Mise en oeuvre de la force brute

Nous comparons simplement chaque requête avec chaque mot du dictionnaire et nous comptons les différentes positions.
Si le nombre ≤ 2, la requête est acceptée.

### Java

"Java
Importation de java.util.*;

solution de classe {
// Compter les erreurs entre deux chaînes de longueur égale
privé int diff(String a, Chaîne b) {
cnt = 0;
pour (int i = 0; i < a.longueur(); i++) {
si (a.charAt(i) != b.charAt(i)) cnt++;
}
retour cnt;
}

liste publique<String> deux requêtesEditWords(String[], dictionnaire String[]) {
Liste <String> ans = nouvelle liste de distribution<>();
pour (String q : requêtes) {
pour (String d : dictionnaire) {
si (diff(q, d) <= 2) {
l'annexe II est modifiée comme suit:
pause; // pas besoin de vérifier plus loin
}
}
}
le retour des an;
}
}
«» "

Python

'`python
Solution de classe:
def twoEditWords(self, requêtes, dictionnaire):
def diff(a, b):
retour sum(1 pour i dans l'intervalle(len(a)) si a[i] != b[i])

ans = []
pour q dans les requêtes :
pour d dans le dictionnaire:
si diff(q, d) <= 2:
(q)
pause
retour et
«» "

C++

'`cpp
#incluez <vecteur>
#incluez <string>

solution de classe {
public:
(const std::string& a, const std::string& b) {
cnt = 0;
pour (size_t i = 0; i < a.size(); ++i)
si (a[i] != b[i]) + cnt;
retour cnt;
}

md::vecteur<std::chaîne> deux requêtesEditWords(std::vector<std::string>,
Std::vector<std::string> dictionnaire) {
md::vecteur<std::chaîne> ans;
pour (const auto& q : requêtes) {
pour (const auto& d : dictionnaire) {
si (diff(q, d) <= 2) {
(q)
pause;
}
}
}
le retour des an;
}
};
«» "

> **Complexité**
> *Temps*: `O(m · n · L)` (m = #queries, n = #dictionnaire)
> *Espace*: "O(1)" (ligner la liste de sortie)

---

La mise en œuvre à trois

La trie nous permet de **explorer tous les mots du dictionnaire qui diffèrent dans au plus deux positions** sans comparer chaque mot.
Nous effectuons une première recherche en profondeur (DFS) sur le tri tout en gardant un compteur du nombre de modifications effectuées jusqu'à présent.

### Java

"Java
Importation de java.util.*;

solution de classe publique {
// -------- Trie noeud - Oui.
Nœud statique privé {
Node[] suivant = nouveau Node[26];
l'extrémité booléenne;
}

// -------- Trie de construction --------
finale privée racine du nœud = nouveau nœud();

vide privé insert(mot d'ordre) {
Noeud cur = racine;
pour (charc : mot.toCharArray()) {
i = c - 'a';
si (cur.next[i] == null) cur.next[i] = nouveau nœud();
cur = cur.next[i];
}
cur.end = vrai;
}

// -------- Recherche DFS...
recherche booléenne privée (noeud, Requête en chaîne, int idx, int édits) {
si (modifications > 2) retourner faux; // prune
si (idx == requête.length()) retourne les modifications <= 2 && node.end;

// Explorer tous les enfants possibles
pour (int i = 0; i < 26; ++i) {
si (node.next[i] == null) continuer;
int nextEdits = éditions + ((char)('a' + i) != requête.charAt(idx) ? 1 : 0);
si (search(node.next[i], requête, idx + 1, nextEdits)) retourne true;
}
retourner faux;
}

liste publique<String> deux requêtesEditWords(String[], dictionnaire String[]) {
// Construire le dictionnaire trie
pour (String w : dictionnaire) insérer(w);

Liste <String> ans = nouvelle liste de distribution<>();
pour (String q : requêtes) {
si (recherche(root, q, 0, 0)) ans.add(q);
}
le retour des an;
}
}
«» "

Python

'`python
Classe TrieNode:
__slots__ = ('enfants', 'fin')
def _init_(self):
l'enfant = [Aucun] * 26
auto.end = Faux

Solution de classe:
def _init_(self):
Self.root = TrieNode()

def insert(self, mot: str):
noeud = self.root
pour ch en mot:
i = ord(ch) - 97
si noeud.enfants[i] n'est pas:
enfants[i] = TrieNode()
noeud = noeud.enfants[i]
noeud.end = Vrai

def search(self, noeud: TrieNode, requête: str, idx: int, édits: int) -> C'est vrai.
si édite > 2: # prune
Retour Faux
Si idx == len(query):
retourner les éditions <= 2 et le noeud. fin
pour i dans la fourchette(26):
enfant = noeud.enfants[i]
si l'enfant n'est pas: continuer
new_edits = éditions + (i != ord(query[idx]) - 97)
if self.search(enfant, requête, idx + 1, new_edits):
retour Vrai
Retour Faux

def twoEditWords(self, requêtes: List[str], dictionnaire: List[str]) -> List[str]:
# Construire le dictionnaire trie
pour w dans le dictionnaire:
auto.insérer(w)

ans = []
pour q dans les requêtes :
si self.search(self.root, q, 0, 0):
(q)
retour et
«» "

C++

'`cpp
#incluez <vecteur>
#incluez <string>
#incluez <mémoire>

struct TrieNode {
std::array<std::unique_ptr<TrieNode>, 26> suivant;
bool end = faux;
};

solution de classe {
public:
std::unique_ptr<TrieNode> racine = std::make_unique<TrieNode>();

oblique insérer(const std::string& word) {
TrieNode* noeud = root.get();
pour (charc : mot) {
i = c - 'a';
si (!node->next[i]) node->next[i] = std::make_unique<TrieNode>();
noeud = noeud->suivant[i].get();
}
noeud->end = vrai;
}

bool dfs(Nœud TrieNode*, const std::string& request,
taille_t idx, modifications d'entrée) {
si (modifications > 2) retourner faux; // taille
si (idx == requête.size()) retourne les modifications <= 2 && noeud->end;

pour (int i = 0; i < 26; ++i) {
TrieNode* enfant = noeud->next[i].get();
si (!enfant) continue;
int nextEdits = éditions + (query[idx] != char('a' + i));
si (dfs(child, requête, idx + 1, nextEdits)) retourne true;
}
retourner faux;
}

md::vecteur<std::chaîne> deux requêtesEditWords(std::vector<std::string>,
Std::vector<std::string> dictionnaire) {
pour (const auto& w : dictionnaire) insérer(w);

md::vecteur<std::chaîne> ans;
pour (const auto& q : requêtes) {
si (dfs(root.get(), q, 0, 0)) ans.push_back(q);
}
le retour des an;
}
};
«» "

> **Complexité**
> *Temps*: `O(L ·=D=" + Q · L)` (L = longueur du mot) – assez rapide même lorsque `L` est jusqu'à 105.
> *Espace*: `O(L ·-D-)` – mémoire pour tous les nœuds triés.

---

Le bon, le mauvais et le mauvais – une liste de contrôle d'entrevue rapide

Étapes Ce que vous avez appris
Il y a un problème.
* Vous pouvez résoudre le problème avec la logique la plus simple. *= Oublier de casser après un match → O(Q·D) * partout *= `break` après le premier match. Autres
*Bad – Trop de branches*= Si vous écrivez un DFS sur tous les mots du dictionnaire, vous pouvez oublier la taille (`edits > 2`) → TLE. Ajouter un garde `si éditer > 2 retourner false`. Autres
*L'Ugly – Structure de données du monde réel*= Quand les contraintes sont plus grandes, la trie est une technique incontournable. Oubliant de marquer les nœuds terminaux → you=ll match *prefixes* incorrectement. S'assurer que `node.end` est vérifié à la feuille. Autres

---

Pourquoi ça compte pour un entretien de codage ? *

1. **Première impression** – Afficher que vous pouvez coder une base **correcte** avant de passer à des optimisations.
2. **Savoirs sur la structure des données** – Les intervieweurs adorent vous voir utiliser un *trie* (ou une carte de hachage avec élagage soigneux) parce que c'est un motif classique pour les problèmes de style de distance de l'edit.
3. **Complicité temporelle** – Mettre en évidence la différence entre "O(Q·D·L)" et "O(L·D + Q·L)" dans votre explication. Il démontre que vous comprenez *pourquoi* une optimisation est utile, pas seulement qu'elle existe.
4. **Gestion des cas** – Mentionnez que tous les mots sont de la même longueur, de sorte que vous n'avez jamais à traiter des insertions/suppressions – seulement des substitutions.
5. **Testing** – LeetCodeLes cas de test sont minuscules, mais toujours écrire des tests unitaires pour vous-même.
"Java
assertion de nouvelle solution().twoEditWords(
Nouvelle chaîne[] {"aaa", "abc"}, nouvelle chaîne[] {"abb", "bbc"}) == Liste. of("aaa", "abc");
«» "

---

## C'est la dernière fois que l'entrevue réussit

Autres Ce que vous vous rappelez Comment ça aide dans une vraie interview
--------------------------------------------------------------------------------------
**Brute-Force** – *quick, correct, fonctionne pour toutes les entrées* Autres
**Trie** – *une structure de données optimisée et classique* Autres
**Les intervieweurs s'attendent à ce que vous parliez de `O(n log n)`, `O(n2)` etc. – ne pas simplement afficher le code, l'expliquer. Autres
Utiliser `_slots__` dans Python, `unique_ptr` dans C++, `private` helpers in Java – une réponse polie vaut 2-3 points supplémentaires. Autres

---

Comment se préparer

1. **Comprendre le code Leet 2452** – Pratiquez les deux approches, puis ajoutez des tests unitaires.
2. **Mise en œuvre de zéro** – Ne pas copier/coller; écrivez la trie vous-même.
3. ** Expliquez votre solution** – Sur papier ou sur tableau blanc, passer par:
* Le compteur d'inadéquation
* Comment les pruneaux DFS après 2 éditions
* Pourquoi `node.end` compte
4. **Run temps-analyse** – Connaître les numéros du pire cas: `m, n ≤ 100`, `L ≤ 100`.
5. **Pensez plus grand** – Mentionnez que pour plus grand `L` (par exemple 105) la trie est essentielle.

---

À emporter

- **La force brute** est *acceptable* pour de petites contraintes et est formidable pour montrer que vous pouvez résoudre le problème fin-fin rapidement.
- **Le tri** est la solution *optimale et conviviale pour les interviews* qui dit aux recruteurs que vous connaissez les structures de données classiques et peut pousser un algorithme à ses limites asymptotiques.

Ajoutez les deux extraits à votre portfolio GitHub, marquez-les avec **`#LeetCode2452 #Trie #JobInterview #Java #Python #C++`**, et vous aurez un point de conversation qui met en valeur à la fois *correctitude* et *efficacité* – le bon endroit que chaque embaucheur cherche. Bon codage !