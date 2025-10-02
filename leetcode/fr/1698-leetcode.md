---
titre: LeetCode 1698. Nombre de sous-chaînes distinctes dans une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1698. Nombre de sous-chaînes distinctes dans une chaîne
**Difficulté:** Moyenne
**Langues:** Java · Python · C++
**Objectif:** Comptez le nombre de sous-chaînes *différentes* qu'une chaîne donnée contient.

> **Pourquoi ça compte pour ta chasse au travail* *
> Les intervieweurs aiment les problèmes qui vous permettent de mettre en valeur *la pensée algorithmique*, *la maîtrise de la structure des données* et *le code propre*.
> Ce problème est un gemme classique – vous pouvez le résoudre avec un jeu simple, une Trie intelligente ou même un suffixe-automaton avancé.
> L'écriture d'une solution claire en trois langues vous prouve que vous êtes à l'aise avec le codage multiplateforme, un must-have pour les rôles supérieurs.

---

La solution Brute-Force / Trie (O(n2))

L'approche Temps Espace
- C'est quoi ?
Autres **Logs de sous-chaînes
**Trie (préfixe-tree)**

La Trie est une version de l'ensemble qui permet d'économiser de l'espace : chaque nouvelle sous-chaîne est représentée par un chemin unique dans l'arbre.
Nous ajoutons seulement un noeud lorsqu'une nouvelle séquence de caractères apparaît pour la première fois, de sorte que le nombre total de nœuds correspond au nombre de sous-chaînes distinctes.

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

---

- Oui. Mise en œuvre Java (Trie)

"Java
Importation de java.util.*;

solution de classe publique {
// Trie node contenant 26 enfants (lettres minuscules)
classe statique privée TrieNode {
TrieNode[] enfant = nouveau TrieNode[26];
}

Nombre d'entrées publiques Distinct(String s) {
TrieNode root = nouveau TrieNode();
Int distinct = 0;

pour (int i = 0; i < s.longueur(); i++) {
TrieNode cur = racine;
pour (int j = i; j < s.longueur(); J++) {
int idx = s.charAt(j) - 'a';
si (cur.child[idx] == null) {
cur.child[idx] = nouveau TrieNode();
distinct++; // Nouvelle sous-chaîne distincte trouvée
}
cur = cur.child[idx];
}
}
retour distinct;
}

// Optionnel: principal pour les tests manuels rapides
public statique vide principal(String[] args) {
System.out.println(nouvelle solution().countDistinct("abba")); // 21
System.out.println(nouvelle solution().countDistinct("abcdefg")); // 28
}
}
«» "

- Oui. Pourquoi c'est **bon* *

- Oui. Pas besoin d'un HashSet supplémentaire ; la mémoire est limitée par les nœuds de Trie.
- Facile à lire.

- Oui. Quoi de neuf?

- Temps encore quadratique ; pour les très longues cordes (n > 105), il sera trop lent.
- La mémoire peut exploser sur les entrées pathologiques (par exemple, tous les caractères uniques).

---

Mise en œuvre de Python (Trie)

'`python
Classe TrieNode:
__slots__ = ("enfant")
def _init_(self):
# 26 lettres minuscules
soi-même.enfant = [Aucun] * 26


Solution de classe:
def countDistinct(self, s: str) -> Int:
racine = TrieNode()
distinct = 0

pour i dans la plage(len(s)):
noeud = racine
pour ch in s[i:]:
idx = ord(ch) - 97 # 'a' -> 0
si noeud.child[idx] n'est pas:
Node.child[idx] = TrieNode()
distinct += 1
noeud = noeud.child[idx]
retour distinct


# Test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.countDistinct("ababa")) # 21
print(sol.countDistinct("abcdefg")) # 28
«» "

- Oui. Points de nettoyage

- "__slots__" garde chaque nœud léger.
- Oui. L'algorithme est identique à Java, juste adapté à la syntaxe de Python.

---

Mise en œuvre C++ (Trie)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct TrieNode {
Enfant de TrieNode*[26];
TrieNode() {
memset(enfant, 0, taille de(enfant);
}
};

solution de classe {
public:
Int countDistinct(chaîne s) {
racine de TrieNode* = nouveau TrieNode();
Int distinct = 0;

pour (size_t i = 0; i < s.size(); ++i) {
TrieNode* cur = racine;
pour (size_t j = i; j < s.size(); ++j) {
int idx = s[j] - 'a';
si (!cur->child[idx]) {
cur->child[idx] = nouveau TrieNode();
+ différent; // Nouvelle sous-chaîne découverte
}
cur = cur->child[idx];
}
}
// (facultatif) Nettoyer la mémoire si vous voulez éviter les fuites.
retour distinct;
}
};

// Démo
Int main() {
Solution sol;
Cout << sol.countDistinct("ababa") << '\n'; // 21
Cout << sol.countDistinct("abcdefg") << '\n'; // 28
retour 0;
}
«» "

> **Astuce:** Dans les environnements de codage concurrentiels, vous ne supprimez généralement pas les nœuds; mais pour un vrai projet, vous avez implémenté une suppression récursive ou utilisez des pointeurs intelligents.

---

C'est pas vrai. Le suivi – O(n) avec un suffixe automaton

Si vous êtes interviewé pour un rôle **Aîné/Lead**, montrant une solution O(n) démontre une connaissance plus approfondie:

"Java
Nombre d'entrées publiques Distinct(String s) {
int n = s.longueur();
int[] lien = nouveau int[2 * n];
int[] len = nouvelle int[2 * n];
int[][] suivant = nouveau int[2 * n][26];
les tableaux.fill(lien, -1);
pour (int i = 0; i < 2 * n; ++i) -1);

int last = 0, taille = 1;
pour (char ch : s.toCharArray()) {
int cur = taille++;
len[cur] = len[dernier] + 1;
int p = dernier;
c = ch - 'a';
pendant que (p != -1 && next[p][c] == -1) {
suivant[p][c] = cur;
p = lien[p];
}
si (p) -1) {
lien[cur] = 0;
} autre {
int q = suivante[p][c];
Si (len[p] + 1 == len[q]) {
link[cur] = q;
} autre {
int clone = taille++;
len[clone] = len[p] + 1;
Système.arraycopy(suivant[q], 0, suivant[clone], 0, 26);
lien[clone] = lien[q];
pendant que (p != -1 && next[p][c] == q) {
suivante[p][c] = clone;
p = lien[p];
}
link[q] = link[cur] = clone;
}
}
dernier = cur;
}

long ans = 0;
pour (int i = 1; i < taille; ++i) ans += len[i] - [lien[i]];
retour (int) ans;
}
«» "

> ** Pourquoi l'utiliser ? **
> - Poignées jusqu'à 106 + confortablement.
> - Montre la connaissance de la théorie des automates – un plus dans les rôles algorithmiques.

---

Article du blog : Le bon, le mauvais et l'horrible sous-chaînes

> **Titre:** *De Tries à Suffix Automata: Maîtriser le nombre de sous-chaînes distinct* Problème

Résumé
Compter des sous-chaînes distinctes est trompeurment simple mais une question d'entrevue de puissance. Il teste votre compréhension des structures de données (ensembles, essais, suffixes arbres/automata), le hachage et la complexité algorithmique. Cet article explore les solutions les plus courantes, leurs compromis et comment les expliquer aux intervieweurs comme un pro.

Mots clés
`#LeetCode #CodingInterview #DistinctSubstrings #Trie #SuffixAutomaton #AlgorithmDesign #Java #Python #C++ "

---

C'est pas vrai. Le "Good" – Un ensemble ou une trie
- **Quoi** : Énumérer chaque sous-chaîne, insérer dans un jeu de hachage, ou construire une Trie pour éviter les duplicatas.
- **Pourquoi**: Simple à implémenter, passe les contraintes de LeetCode (n ≤ 500).
- **Résultat**: temps `O(n2)`, mémoire `O(n2)`
*Idéal pour gagner rapidement ou quand les contraintes sont modestes. *

C'est vrai. L'Éclat – Temps Quadratique avec le Hash Rolling
- **Quoi**: Générer tous les sous-chaînes, calculer un hachage roulant (par exemple, Rabin‐Karp), insérer dans un ensemble de hachage.
- **Pourquoi**: constantes légèrement plus rapides qu'un ensemble de cordes, mais toujours `O(n2)`.
- **Résultat**: toujours quadratique, risque de collisions de hachage, code plus complexe.
*Ne vaut pas le code supplémentaire à moins d'éviter l'attribution de chaînes. *

C'est vrai. L'Arbre de suffixe (trop lourd)
- **Quoi**: Construire un suffixe, puis compter les bords des feuilles.
- **Pourquoi**: Historiquement la solution du manuel ('O(n)').
- **Résultat**: La mise en œuvre est longue (~200 lignes), difficile à déboguer, rarement nécessaire sur LeetCode.
*Le mieux évité à moins que vous soyez vraiment prêt à prouver la maîtrise des structures de données avancées. *

C'est pas vrai. L'Héroïque – suffixe Automaton (O(n))
- **Quoi**: Construire un DFA minimal qui reconnaît tous les suffixes; le nombre de sous-chaînes distinctes est égal à la somme sur les états de «len[state] - len[state]»».
- **Pourquoi**: Temps linéaire, mémoire linéaire. Il gère des cordes jusqu'à des millions de caractères.
- **Résultat**: Un code concis et intelligent qui impressionne les intervieweurs seniors.
*Si vous pouvez l'expliquer en anglais, vous êtes une coupe au-dessus du reste. *

---

C'est pas vrai. Comment parler Dans une interview

1. **Démarrer Simple* *
*=I=ll d'abord implémenter une Trie parce qu'il est intuitif et fonctionne pour les contraintes données.
2. **Mentionner le suivi**
Si nous devions traiter de très longues chaînes, nous passerions à un suffixe automatique pour le temps linéaire.
3. **Exposer la complexité**
*La Trie donne du temps à O(n2) ; l'automate le réduit à O(n) en réutilisant des suffixes déjà vus.
4. **Lisez le code* *
*Utilisez des commentaires, `__slots__` et des noms de variables clairs. *
5. **Relativement au monde réel* *
Dans les moteurs de recherche ou le séquençage du génome, nous avons souvent besoin de compter des modèles distincts efficacement, donc suffixe automate sont pratiques.

---

## 8.-SEO-Takeaway optimisé

- **Mots-clés**: LeetCode 1698, Solution de sous-chaînes distinctes, Découpe vs suffixe automate, Découper les sous-chaînes distinctes, Découper les sous-chaînes.
- **Meta Description**: -Solve LeetCode 1698 (Nombre de sous-chaînes distinctes) avec code Java, Python et C++ propre. Comparez Trie, Rolling Hash et l'approche Suffix Automaton linéaire. (en milliers de dollars)
- ** Hiérarchie du contenu** : Effacer les rubriques (`H1`, `H2`, `H3`) pour augmenter la lisibilité du moteur de recherche.

---

Appel à l'action
> * Prêt à accepter votre prochaine entrevue de codage? Attrapez les extraits de code, pratiquez les expliquer, et laissez le problème des sous-chaînes distinctes devenir votre arme secrète. *

---

**Fin de l'article**

N'hésitez pas à copier, adapter et publier sur votre blog ou Linked Pour attirer les recruteurs à la recherche d'experts en algorithme. Bonne chance ! C'est ce qu'il a dit.

---

**#Réponse** – Le problème peut être résolu dans les trois langues avec une trie. Pour les contraintes plus grandes, montrez l'automate de suffixe O(n). Le blog ci-dessus explique les compromis, prêts pour l'interview narrative et la visibilité du référencement.