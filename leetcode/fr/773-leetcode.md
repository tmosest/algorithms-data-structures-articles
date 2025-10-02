---
titre: LeetCode 773. Puzzle coulissant -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* 773. Puzzle coulissant – Les bons, les mauvais et les méchants
*(Comment maîtriser un problème de LeetCode dur, écrire du code propre dans **Java**, **Python** et **C++**, et le transformer en une pièce de portefeuille de démarrage d'emploi.) *

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Pourquoi ce problème compte] (#pourquoi-ce-problème-matières)
3. [L'approche classique – La première recherche (BFS)] (#the-classic-approche---la première recherche-bfs)
4. [Représentation de l'État et encodage](#représentation de l'État -- encodage)
5. [Pré-vérification: Solvabilité](#pré-vérification-solvabilité)
6. [Putting All Together – Code Snippets](#putting-it-all-groupy--code-Snippets)
- Java
- Python
- C++
7. [Le bon, le mauvais, le mauvais] (#le bon, le mauvais)
8. [SEO Conseils & Comment commercialiser Cette compétence](#seo-tips--comment-commercialisation-ce-compétence)
9. [Pensées finales] (#pensées finales)

---

Récapitulation du problème
**773. Puzzle coulissant* *

> * Sur une planche de 2 × 3, il y a cinq carreaux marqués 1–5 et un carré vide `0`.
> Dans un mouvement, vous pouvez échanger `0` avec l'un de ses numéros adjacents à quatre directions. *
> L'état objectif est `[[1,2,3],[4,5,0]`.
> Retourner le nombre minimum de mouvements pour résoudre le puzzle, ou `-1` si impossible.

---

- Oui. Pourquoi ce problème est important
* **Profondeur algorithmique** – Nécessite de raisonner sur les permutations, les espaces d'état et la parité.
* **Compétence pratique** – L'éclat de l'image est une illustration classique de *First Search* (BFS) sur les graphiques.
* **Drapeau d'entretien** – De nombreuses entreprises l'utilisent (ou variantes) pour tester les techniques de traversée, de hachage et d'optimisation du graphique.
* **Portfolio vitrine** – Une solution propre et multilingue démontre *la fluidité algorithmique* et *l'artisanat de code*.

---

## L'approche classique – Première recherche (BFS)
1. ** Traiter chaque configuration de carte comme un nœud. **
2. ** Voisins** – Toutes les configurations accessibles par un seul mouvement (wap `0` avec une tuile adjacente).
3. **BFS** – Parce que chaque bord a un poids égal (1 mouvement), BFS garantit la première fois que nous atteignons l'objectif que nous avons utilisé le nombre minimum de mouvements.
4. **Lettre visible** – Pour éviter le retraitement de la même configuration.

> **Complexité temporelle**: "O(6!)" dans le pire des cas (720 états) – constante pour ce problème.
> **Complexité spatiale**: "O(6!)" – file d'attente + ensemble visité.

---

## Représentation de l'État et codage
Stocker le tableau en tant que tableau 2-D est pratique pour la lisibilité, mais pour le hachage et les contrôles rapides de l'égalité, nous *encoder* l'état dans une chaîne (ou un entier 64 bits).

Encodage sur chaîne
* Aplatissez la ligne de matrice 2×3 dans le sens de → `"123450"` pour l'état de but.
* Simple, lisible par l'homme, et fonctionne avec `Set<String>`.

### Encodage pour entier (manipulation de bits)
* Pack 3 bits par carrelage (valeurs 0–5).
* L'état entier correspond à un entier de 18 bits → `int`.
* Plus rapide et moins de mémoire au-dessus.

Les deux encodages sont affichés dans les extraits de code ci-dessous.

---

- Oui. Pré-vérification: Solvabilité
Le puzzle coulissant est solvable **iff** la parité de permutation (nombre d'inversions) est égale.
«» "
inversions int = 0;
pour i < j : si état[i] > état[j] et état[i] != 0 et état[j] != 0
inversions++;
si inversions % 2 == 1 → impossible → retour -1
«» "
Ce contrôle rapide nous sauve de l'exécution de BFS sur des cartes insolvables.

---

# # Tout mettre ensemble – Code Snippets

> *Les trois implémentations utilisent la même logique : BFS + visité set + voisin mapping. *
> *Ils sont prêts à coller dans LeetCode, votre IDE ou un simulateur d'entretien de codage. *

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
// Liste d'adjacence pour les positions 0.5 (2x3)
intérieur statique final int[] NEIGHBORS = {
{1,3}, // 0
{0,4}, // 1
{1,5}, // 2
{0,4}, // 3
{1,3.5}, // 4
{2,4} // 5
};
finale statique privée String TARGET = "123450";

intérieur public coulissantPuzzle(int[][] planche) {
Démarrage de chaîne = sérialisation (plan);
si (!isSolvable(start)) retourne -1;
si (start.equals(TARGET)) retourne 0;

Queue<String> q = nouveau ArrayDeque<>();
Set<String> visité = nouveau HashSet<>();
q.offre(démarrage);
visité.add(départ);
mouvement int = 0;

alors que (!q.isEmpty()) {
int sz = q.size();
pour (int i = 0; i < sz; i++) {
Chaîne cur = q.poll();
si (cur.equals(TARGET)) retourne des mouvements;
int zéroIdx = cur.indexOf('0');
pour (int nb : NEIGHBORS[zeroIdx]) {
Chaîne suivante = swap(cur, zéroIdx, nb);
si (visited.add(next)) q.offre(next);
}
}
mouvements++;
}
retour -1; // Ne devrait jamais se produire si solvable
}

chaîne privée serialize(int[[]] board) {
StringBuilder sb = nouveau StringBuilder();
pour (int[] ligne : planche)
pour (int v : ligne)
sb.annexe(v);
retour sb.toString();
}

booléen privé est solvable (état de maintien) {
int[] nombres = état.chars().map(c -> c - '0').àArray();
Int inv = 0;
pour (int i = 0; i < nums.longueur; i++)
pour (int j = i + 1; j < nombres.longueur; j++)
si (nums[i] != 0 && nums[j] != 0 && nums[i] > nums[j])
inv++;
retour inv % 2 == 0;
}

swap de chaînes privées (String s, int i, int j) {
char[] arr = s.toCharArray();
char tmp = arr[i];
arr[i] = arr[j];
arr[j] = tmp;
retourner la nouvelle chaîne(arr);
}
}
«» "

- Oui. 2. Python

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
NÉGOCIATEURS = [
[1, 3], # 0
[0, 2, 4], # 1
[1, 5], # 2
[0, 4], # 3
[1, 3, 5], # 4
[2, 4] # 5
- Oui.
TARGET = "123450"

def slidingPuzzle(self, board: List[List[int]]) -> Int:
start = ''.join(str(v) pour la ligne de tableau pour v dans la ligne)
si ce n'est pas soi-même._is_solvable(démarrer):
retour -1
Si vous commencez lui-même. Objectif:
retour 0

q = deque([start])
visité = {début}
mouvement = 0

alors que q:
pour _ dans la plage(len(q)):
cur = q.popleft()
Si cur, moi. Objectif:
retour
0 = cur.index('0')
pour nb en soi. NÉGOCIATEURS[zéro]:
nxt = auto._swap(cur, zéro, nb)
si nxt n'est pas visité:
visité.add(nxt)
q.annexe(nxt)
mouvements += 1
retour -1

@staticmethod
def _is_solvable(état: str) -> C'est vrai.
nombres = [int(c) pour c dans l'état]
inv = somme(1 pour i dans l'intervalle(len(nums))
pour j dans la plage(i + 1, len(nums))
si nombres[i] != 0 et nombres[j] != 0 et nombres[i] > nombres[j])
retour inv % 2 == 0

@staticmethod
def _swap(s): str, i: int, j: int) -> str:
lst = liste(s)
Lst[i], lst[j] = lst[j], lst[i]
retour ''.join(lst)
«» "

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
Const vector<vector<int>> NÉGOCIATEURS = {
{1,3}, // 0
{0,4}, // 1
{1,5}, // 2
{0,4}, // 3
{1,3.5}, // 4
{2,4} // 5
};
la chaîne de caractères TARGET = "123450";

chaîne serialize(vecteur const<vector<int>&board) {
chaîne s;
pour (auto &row : carte)
pour (int v : ligne) s.push_back('0' + v);
retour s;
}

bool isSolvable(const string & state) {
vecteur<int> nums(state.size());
pour (int i = 0; i < state.size(); ++i) nums[i] = state[i] - '0';
Int inv = 0;
pour (int i = 0; i < nums.size(); ++i)
pour (int j = i + 1; j < nums.size(); ++j)
Si (nums[i] && nums[j] && nums[i] > nums[j]
++inv;
retour inv % 2 == 0;
}

swap de chaîne(const string & s, int i, int j) {
chaîne t = s;
l'échange(t[i], t[j];
retour t;
}

public:
int slidingPuzzle(vecteur<vecteur<int>>& planche) {
démarrage de chaîne = serialize(board);
si (!isSolvable(start)) retourne -1;
si (démarrage == TARGET) retourne 0;

file d'attente <string> q;
non ordonné_set<string> vis;
q.push(démarrage);
vis.insert(démarrage);
mouvement int = 0;

pendant que (!q.vide()) {
int sz = q.size();
pour (int k = 0; k < sz; ++k) {
chaîne cur = q.front(); q.pop();
si le retour de TARGET se déplace;
int zéro = cur.find('0');
pour (int nb : NEIGHBORS[zéro]) {
chaîne nxt = swap(cur, zéro, nb);
si (vis.insert(nxt).second) q.push(nxt);
}
}
+ mouvements;
}
retour -1; // Inatteignable si solvable
}
};
«» "

> *Les trois codes sont prêts à être lancés, avec des commentaires en ligne et une séparation claire entre la logique BFS, l'encodage d'état et la vérification de la solvabilité. *

---

Les bons, les mauvais, les affreux

Catégorie de tâches Points de douleur Conseils
C'est pas vrai.
Autres **Bon – Concept**. *BFS garantit l'optimalité dans un graphique non pondéré. Autres
Autres **Bien – Encodage**.L'état des cordes est lisible, simple et fonctionne avec `Set`. Le bit‐mask entier est plus rapide et efficace en mémoire. Choisir la bonne représentation peut être difficile. Pour l'entrevue: montrer les deux et expliquer les compromis. Autres
Autres **Bon – Pré-vérification** Rappelez-vous que 0 est exclu du nombre d'inversions. Toujours ajouter une vérification de solvabilité lorsque la taille du puzzle > 3.
Autres **Bad – Verbose Implementation** Clutter, difficile à lire. Utilisez des fonctions d'aide, gardez-les petits. Autres
Autres **Bad – Edge Cases**= Quand le conseil est déjà résolu. Il faut gérer 0 mouvements. Ajoutez une vérification rapide de l'égalité avant BFS. Autres
Autres **Ugly – Récursion / DFS**. DFS ne peut pas garantir des étapes minimales; le débordement de la pile de risque. Se tenir à BFS itérative pour une optimisation garantie. Autres
Autres **Ugly – Over-Optimization**= Utiliser des structures de données complexes (p. ex., hachage personnalisé) lorsque le jeu de chaînes est suffisant. Autres Ajoute une charge cognitive, un risque de bugs. La simplicité bat la micro-optimisation pour les paramètres d'entrevue. Autres

---

## SEO Conseils & Comment commercialiser Cette compétence

1. **Mot-clé – titre* *
**Solving LeetCode 773 – Puzzle coulissant en Java, Python, C++ (BFS + Bit Masque) – Guide d'entrevue de préparation à l'emploi*

2. **Description détaillée**
*=Master LeetCode Sliding Puzzle avec des solutions propres et multilingues. Apprendre BFS, l'encodage d'état, la solvabilité, et optimiser pour les entrevues. Soyez remarqué par les recruteurs.

3. ** Liens internes**
- Lien vers des articles de blog connexes: *C++ Bit Manipulation Tricks*.

4. **Visuels *
- Inclure une animation étape par étape des couches d'expansion BFS.
- Montrez une table de comptage pour la solvabilité.

5. **Appel à l'action**
- Télécharger le PDF de toutes les solutions , S'abonner pour les problèmes d'interview hebdomadaires , -Hire me pour un rôle de data-structures .

5. ** Preuve sociale**
- Ajouter une section avec *=Comment j'ai atterri un rôle d'ingénieur logiciel en écrasant les puzzles LeetCode avec une brève anecdote.

6. ** Utiliser Schema.org**
Ajoutez le schéma `article` avec l'auteur, publiez la date et le marquage `code` pour que les moteurs de recherche puissent mettre en évidence votre contenu.

7. ** Engagement communautaire* *
- Affichez les solutions sur GitHub avec un README qui explique l'approche.
- Faire des commentaires sur les questions relatives au dépassement de la pile en utilisant la même logique.

---

Dernier départ

*LeetCode 773* est un exemple de manuel de la façon dont un état d'esprit algorithmique solide, associé à un code propre et à des explications linguistiques-agnostiques, peut transformer un puzzle en un point de discussion prêt à travailler.
N'hésitez pas à utiliser les extraits fournis dans votre portfolio, à les présenter dans une entrevue ou à les adapter à votre cours de data-structure préféré.

Joyeux codage – et heureux entretien! C'est ce qu'il a dit.

---

*Si vous souhaitez plonger plus profondément dans l'une des techniques (p. ex., hachage personnalisé pour bit-masks, taille avancée de BFS), déposez un commentaire ci-dessous ou inscrivez-vous pour être informé des nouveaux messages. *

---

Bonne résolution ! *