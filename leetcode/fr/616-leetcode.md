---
titre: LeetCode 616. Ajouter une étiquette gras dans la chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Ajouter une étiquette forte dans la chaîne – LeetCode 616
**Les solutions Java, Python & C++ + un guide d'interview -Bon-Bad-Ugly**

> **Meta-description** – Vous cherchez à faire votre prochaine entrevue de codage? Master LeetCode 616 – *Ajouter une étiquette forte dans la chaîne*. Plongez dans une implémentation propre de Trie, un tour de booléenne et une version C++. Préparez-vous à l'emploi avec les idées d'entrevues bonnes, mauvaises et laides.

---

- Oui. 1. Déclaration de problème

> Vu une chaîne `s` et un tableau de chaînes `words`, wrap **chaque sous-chaîne** de `s` qui apparaît dans `words` avec une seule paire de balises gras `<b>` ... `</b>`.
> • Si deux sous-chaînes se chevauchent, fusionnez-les en un bloc gras.
> • Si deux blocs gras sont consécutifs, fusionnez-les aussi.

**Exemple**

«» "
Entrée: s = "aaabbb", mots = ["aa","b"]
Sortie: "<b>aaabbb</b>"
«» "

**Contrôles* *

- `1 <= longueur <= 1000`
- `0 <= words.longueur <= 100`
- `1 <= mots[i].longueur <= 1000`
- `s` et tous les `words[i]` ne contiennent que des lettres et des chiffres anglais.

Le problème est une question d'interview classique sur les chaînes de caractères; c'est aussi la base du LeetCode.

---

- Oui. 2. Aperçu de la solution

Le principal défi est de ** trouver efficacement toutes les occurrences des mots** dans `s`, puis de fusionner les intervalles de chevauchement/de rapprochement. Deux approches populaires :

L'approche du cœur Idée du temps Espace
- C'est quoi ?
Autres **Trie + Scan**.Construisez un tri de tous les mots; à chaque index de `s` marcher le trie pour trouver le plus long match. Marquer un tableau booléen pour les positions de "bold". Autres
Pour chaque mot, scannez `s` avec `indexOf`; marquez les plages correspondantes. Autres

Nous nous concentrons sur l'implémentation **Trie** – elle est concise, fonctionne rapidement et démontre une structure de données classique. Nous montrons également la variante **boolean array** pour l'exhaustivité.

---

- Oui. 3. Bonne, mauvaise et laid – Points d'entrevue

Qu'est-ce que mettre en avant?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Clarifier le format d'entrée** Oublier de gérer les mots vides → 'O(0)` Vérifier la longueur des mots. 0` → retourner `s`
Autres 2= **Définition =========================================================================================================================================================================================================================================================
**Cas d'Edge avec gras consécutif** Parce que `3 == 2+1`=0 Oubliant de fusionner → tags de brouillage
Autres 4= ** justification de la complexité**= Montrer comment la trie réduit le pire des cas de `O(n*m)` à `O(n * maxLen)` Sur-optimisation en cachant le plus long match par index.
*Test** * Inclure les cas où les mots se chevauchent, les mots imbriqués et les mots identiques.

> Une explication claire de l'algorithme, une manipulation soigneuse des indices et une complexité prouvée liée.
> *Bad** – Une implémentation trop verbeuse qui oublie de fusionner des intervalles ou mal gérer le dernier bloc gras.
> **Ugly** – Brute-force imbriqué boucles avec concaténation de cordes à l'intérieur; il fonctionne mais temps-out sur le grand jeu de tests.

---

- Oui. 4. Extraits de code

Voici les solutions **complètes, prêtes à composer** dans **Java**, **Python** et **C++**. Tous les trois utilisent l'approche Trie; la solution Python inclut également une variante alternative de l'arrachage booléen pour la comparaison.

Autres **Tout le code est testé sur la plateforme LeetCode. **
Autres **Rappelez-vous de coller le code dans la section de langue correspondante sur LeetCode. **

---

#### 4.1 Java – Mise en œuvre des essais

"Java
// Java 17

Importation de java.util.*;

solution de classe {

- Oui. Trie Node --------- */
classe statique privée TrieNode {
Carte <Character, TrieNode> enfant = nouveau HashMap<>();
booléen isWord = faux;
}

- Oui. Essai --------- */
classe statique privée Trie {
racine de TrieNode finale privée = nouveau TrieNode();

vide ajouter (mot d'ordre) {
TrieNode noeud = racine;
pour (charc : mot.toCharArray()) {
noeud = noeud.child.computeIfAbsent(c, k -> nouveau TrieNode());
}
noeud. isWord = vrai;
}

/* Retourner le dernier index (inclus) du mot le plus long
qui commence à la position 'départ' dans 's'.
Si aucune, retourner -1. */
int le plus long Match(String s, démarrage int) {
TrieNode noeud = racine;
Int fin = -1;
pour (int i = début; i < s.longueur(); i++) {
c = s.charAt(i);
noeud = noeud.child.get(c);
si (noeud == nul) rupture;
si (node.isWord) fin = i;
}
fin de retour;
}
}

chaîne publique addBoldTag(chaîne s, chaîne[] mots) {
if (mots == null="words.longueur == 0) retour s;

Trie trie = nouveau Trie();
pour (String w : mots) trie.add(w);

int n = s.longueur();
booléen[] gras = nouveau booléen[n];
int maxEnd = -1; // position la plus rapprochée jusqu'à présent

pour (int i = 0; i < n; i++) {
int fin = trie.longest Match(s, i); // mot le plus long commençant par i
maxEnd = Math.max(maxEnd, fin); // fusionner avec l'intervalle précédent
bold[i] = maxEnd >= i; // la position actuelle est bold
}

StringBuilder sb = nouveau StringBuilder();
booléen inBold = faux;
pour (int i = 0; i < n; i++) {
si (bold[i] & & & &!inBold) { // commencer en caractères gras
sb.append("<b>");
inBold = vrai;
} sinon si (!bold[i] && inBold) { // fin bold
sb.append("</b>");
inBold = faux;
}
sb.append(s.charAt(i));
}
si (inBold) sb.append("</b>"); // fermer à la fin
retour sb.toString();
}

- Oui. Pilote simple pour les essais locaux
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.addBoldTag("abcxyz123", nouvelle chaîne[]{"abc","123"});
Système.out.println(sol.addBoldTag("aaabbb", nouvelle chaîne[]{"aa","b"});
}
}
«» "

**Complexité* *
- Temps: `O(=" * maxLen(words))` – chaque index scanne au plus le mot le plus long.
- Espace: `O(totalLength(words) +="s=")` – nœuds triés + tableau booléen.

---

#### 4.2 Python – Variante Trie & Booléenne-Array

'`python
# Python 3.11

Classe TrieNode:
__slots__ = ("enfant", "is_word")
def _init_(self):
l'enfant = {}
Self.is_word = Faux

Classe Trie:
def _init_(self):
Self.root = TrieNode()

def add(self, mot: str):
noeud = self.root
pour ch en mot:
noeud = noeud.child.setdefault(ch, TrieNode())
node.is_word = Vrai

def least_match(self, s: str, start: int) -> Int:
noeud = self.root
fin = -1
pour i dans la plage (départ, len(s)):
noeud = noeud.child.get(s[i])
si le nœud n'est pas :
pause
si node.is_word:
fin = i
retour fin

Solution de classe:
def addBoldTag(self, s: str, words: list[str]) -> str:
si ce n'est pas des mots:
retour s

trie = Trie()
pour w en mots:
trie.add(w)

n = len(s)
bold = [Faux] * n
_Fin max = -1
pour i dans la plage(n):
fin = trie.longest_match(s, i)
max_end = max(max_end, fin)
bold[i] = max_end >= Les

res = []
_bold = Faux
pour i, ch dans le(s) énuméré(s):
si bold[i] et non in_bold:
res.append("<b>")
in_bold = Vrai
elif not bold[i] et in_bold:
res.append("</b>")
_bold = Faux
res.append(ch)
si in_bold :
res.append("</b>")
retourner "".join(res)

C'est... Force brute booléenne (pour comparaison) ---------
def addBoldTag_bruteforce(s): str, mots: list[str]) -> str:
n = len(s)
bold = [Faux] * n
pour w en mots:
début = s.find(w)
tout en commençant != - 1 :
pour i dans la plage (départ, début + len(w)):
bold[i] = Vrai
début = s.find(w, début + 1)
res, in_bold = [], Faux
pour i, ch dans le(s) énuméré(s):
si bold[i] et non in_bold:
res.append("<b>")
in_bold = Vrai
elif not bold[i] et in_bold:
res.append("</b>")
_bold = Faux
res.append(ch)
si in_bold :
res.append("</b>")
retourner "".join(res)

♪ - Oui. Conducteur simple...
si __nom__ == "__main__" :
sol = Solution()
print(sol.addBoldTag("abcxyz123", ["abc","123"])
print(sol.addBoldTag("aaabbb", ["aa","b"])
«» "

**Notes**

- `__slots__' réduit les frais de mémoire pour le tri.
- La variante de force brute est "O(len(words) * len(s)" et doit être évitée dans la production.

---

### 4.3 C++ – Mise en œuvre des essais

'`cpp
// C++17 (GNU++17)

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct TrieNode {
tableau <TrieNode*, 62> enfant; // 0-9, A-Z, a-z
bool isWord;
TrieNode() : child{nullptr}, isWord(false) {}
};

classe Trie {
racine de TrieNode* = nouveau TrieNode();
public:
vide add(const string& word) {
TrieNode* noeud = racine;
pour (char ch : mot) {
idx = charIndex(ch);
si (!node->child[idx]) node->child[idx] = nouveau TrieNode();
noeud = noeud->enfant[idx];
}
noeud->isWord = vrai;
}

/* Retourner le dernier index du match le plus long à partir de 'start'.
Retourner -1 si aucune correspondance. */
int le plus long Match(const string& s, int start) const {
TrieNode* noeud = racine;
Int fin = -1;
pour (int i = début; i < (int)s.size(); ++i) {
int idx = charIndex(s[i]);
noeud = noeud->enfant[idx];
Si (!noeud) casse;
si (node->isWord) fin = i;
}
fin de retour;
}

particulier:
// Carte: '0'-'9' -> 0-9, 'A'-'Z' -> 10-35, 'a'-'z' -> 36-61
int statique charIndex(char c) {
si ('0' <= c && c <= '9') retourner c - '0';
si ('A' <= c && c <= 'Z') retourner 10 + (c - 'A');
retour 36 + (c - 'a');
}
};

solution de classe {
public:
chaîne addBoldTag(chaîne s, vector<chaîne> mots) {
si (words.vide()) retourne s;

Trie trie;
pour (const auto& w : mots) trie.add(w);

int n = s.size();
vecteur<bool> bold(n, false);
l'ent maxEnd = -1;
pour (int i = 0; i < n; ++i) {
int fin = trie.longest les correspondances, i);
maxEnd = max(maxEnd, fin);
bold[i] = (maxEnd >= i);
}

la chaîne rés;
bool inBold = faux;
pour (int i = 0; i < n; ++i) {
si (bold[i] & & &!inBold) { res += "<b>"; inBold = true; }
si (!bold[i] && inBold) { res += "</b>"; inBold = false; }
res += s[i];
}
si (inBold) res += «</b>»;
retour rés;
}
};
«» "

**Complexité** – identique à la version Java.

En C++ vous pouvez optimiser le trie avec un tableau de 62 enfants (10+26+26).

---

- Oui. 5. À emporter pour l'interview

- **Expliquer l'algorithme étape par étape** (construire, scanner, marquer, fusionner).
- **Validez les cas de bord** (vides `mots`, mots à caractère unique, intervalles recoupants).
- ** Mettre en évidence l'échange espace/temps de la trie.
- **Afficher un pilote minimum** ou une fonction `main` si vous codez en dehors de LeetCode; il démontre la confiance.

Souvenez-vous, les compteurs LeetCodes **runtime** et **Memory** sont stricts. Une solution qui fusionne les intervalles paresseusement (à la volée) et ** insère les balises dans un seul passage** passera tous les tests.

---

- Oui. 6. La pensée finale

> **Bold Words in String** est l'équivalent d'une entrevue de codage d'un problème de la meilleure pratique*. Mastering the trie scan + interval merge pattern non seulement vous obtient à travers LeetCode, mais prouve également votre capacité à gérer le prétraitement de la chaîne, recherche efficace, et la logique de bordure prudente – compétences chaque ingénieur logiciel senior doit posséder.

Bon codage et bonne chance à votre prochaine interview! C'est ce qu'il a dit.

---

Les Vous avez des questions ? * *
- Tu veux une solution Rust ?
- Curieux à propos d'Aho-Corasick pour l'appariement multi-pattern ?

Faites-moi savoir dans les commentaires – Je vais mettre à jour la repo avec plus de langues!