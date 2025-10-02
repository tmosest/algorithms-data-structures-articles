---
titre: LeetCode 2049. Nombre de nœuds avec le score le plus élevé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
C'est pas vrai. Solutions en trois langues pour LeetCode 2049
**=Count nœuds avec le score le plus élevé**– O(n) DFS

Code de la langue
C'est quoi, ça ?
**Java** Cliquez pour agrandir</résumé>

"Java
Importation de java.util.*;

solution de classe {
/** Solution DFS O(n) pour LeetCode 2049 */
Nombre d'entrées publiquesHighestScoreNodes(int[] parents) {
int n = parents.longueur;
// Créer une liste d'adjacence
Liste <entier>[] enfants = nouvelle liste de répartition;
pour (int i = 0; i < n; i++) les enfants[i] = nouvelle liste de distribution<>();
pour (int i = 1; i < n; i++) enfants[parents[i]].add(i);

long maxScore = 0;
int mieux Cnt = 0;
dfs(0, enfants, n, maxScore, bestCnt);
le meilleur retour Cnt;
}

// DFS qui retourne la taille du sous-arbre enraciné à `node "
int privé dfs(int node, Liste<integer>[] enfants, int n,
long maxScore, int bestCnt) {
long score = 1;
int sum = 0; // nombre de nœuds dans tous les sous-arbres d'enfants

pour (int enfant : enfants[node]) {
int sz = dfs(enfant, enfants, n, maxScore, bestCnt);
score *= sz; // multiplier par la taille de chaque sous-arbre d'enfant
somme += sz;
}

int repos = n - somme - 1; // noeuds qui restent lorsque le noeud courant est enlevé
si (rest > 0) score *= repos;

si (score > maxScore) {
maxScore = score;
bestCnt = 1;
} sinon si (score == maxScore) {
bestCnt++;
}

somme de retour + 1; // taille du sous-arbre actuel
}
}
«» "
</détails>
**Python**=Détails><résumé>Cliquez pour agrandir</résumé>

'`python
Solution de classe:
def countHighestScoreNodes(self, parents: List[int]) -> Int:
n = len(parents)
# liste d'adjacence
enfants = [[] pour _ dans l'intervalle(n)]
pour i dans la plage (1, n):
enfants[parents[i]].annexe(i)

auto.max_score = 0
autorésultats = 0

def dfs(node: int) -> Int:
score = 1
total = 0 # noeuds dans les sous-arbres d'enfants
pour les enfants[node]:
sz = dfs(enfant)
score *= sz
Total += sz

repos = n - total - 1
en cas de repos > 0:
score *= repos

si score > self.max_score:
auto.max_score = score
résultat personnel = 1
score elif == self.max_score:
soi-même. résultat += 1

total de retour + 1 # taille de ce sous-arbre

dfs(0)
Revenez vous-même. résultat
«» "
</détails>
**C++** Cliquez pour agrandir</résumé>

'`cpp
solution de classe {
public:
nombre intHighestScoreNodes(vecteur<int> et parents) {
int n = parents.size();
vecteur<vecteur<int>> enfant(n);
pour (int i = 1; i < n; ++i) enfant[parents[i]].push_back(i);

long maxScore = 0;
réponse int = 0;

fonction<int(int)> dfs = [&](inint node) -> Int {
long score = 1;
int sum = 0; // noeuds dans les sous-arbres enfants
pour (int ch : enfant[node]) {
int sz = dfs(ch);
score *= sz;
somme += sz;
}
inter repos = n - somme - 1; // noeuds restants lorsque ce noeud est enlevé
si (rest > 0) score *= repos;

si (score > maxScore) {
maxScore = score;
réponse = 1;
} sinon si (score == maxScore) {
++réponse;
}
somme de retour + 1; // taille du sous-arbre actuel
};

dfs(0);
réponse de retour;
}
};
«» "
</détails>

> **Pourquoi O(n) fonctionne**
> Chaque nœud est visité exactement une fois.
> - Construire la liste d'adjacence est **O(n)**.
> - La DFS calcule les dimensions des sous-arbres en une seule passe post-commande – encore une fois **O(n)**.
> La seule opération lourde est la multiplication d'au plus 2 × 105 numéros, qui s'adapte facilement en 64 bits (long'/long').

> ** La main dans la racine**
> La racine n'a pas de sous-arbre parent.
> Dans la formule `rest = n - total - 1`, `rest` est zéro pour la racine (il n'y a pas de nœud au-dessus).
> Nous multiplions par `rest` seulement quand il est > 0; sinon nous ignorons simplement ce facteur – cela maintient le score correct pour la racine.

> **Liste de contrôle des cas* *
> * `n = 2` – seulement la racine et une feuille; score = 1, réponse = 1.
> * Tous les nœuds sont des feuilles – chaque score = 1, réponse = n.
> * Arbre très déséquilibré (une chaîne) – le « repos » peut être zéro plusieurs fois, mais la logique fonctionne encore.

> ** Pièges communs* *
> 1. L'utilisation de `int` pour le score peut déborder (le score maximum peut être ~2 × 1010).
> 2. Oubliant de soustraire le nœud actuel (`-1`) lors du calcul du "rest".
> 3. Décommander le DFS (précommande vs postcommande) – vous devez d'abord connaître la taille des enfants avant de calculer le score des nœuds.

> **Heure et espace**
> * Heure :* **O(n)* *
> *Space:* **O(n)** pour la liste d'adjacence + pile de récursions.

---

Article de blog optimisé par le SEO – Code Leet 2049 Explique : C'est bien, c'est mal.

> **Mots clés**: *LeetCode 2049, Noeuds de comptage avec le plus haut score, arbre binaire DFS, O(N) algorithme, problème de codage d'entrevue, entretien d'ingénieur logiciel, conseils d'entrevue technique, conception d'algorithme, préparation d'entrevue d'emploi. *

---

Introduction
Si vous êtes à la poursuite de votre premier rôle d'ingénierie logicielle ou de brossage pour une entrevue de codage, **LeetCode 2049 – - Avec le score le plus élevé** est un problème classique qui teste votre compréhension des arbres, la récursion, et arithmétique soigneuse. Ci-dessous, nous disséquons le problème, marchons à travers une solution O(n) propre, et mettons en évidence ce qui en fait une *grande question d'entrevue* (le "bon"), quels pièges maintiennent les candidats coincés (le "bad"), et les courants de désordre qui peuvent conduire aux bugs (le "ugly").

---

Déclaration de problème
> On vous donne un arborescence binaire des nœuds `n` (0-based indexing) décrits par le tableau `parents`, où `parents[i]` est le parent du noeud `i` (la racine a `-1`).
> Pour chaque nœud, vous le retirez et calculez le produit des tailles de tous les composants connectés résultants.
> Le *score* d'un noeud est ce produit.
> **Tâche**: Retournez le nombre de nœuds qui obtiennent le score le plus élevé.

---

###  uvre principale – DFS + taille du sous-arbre
Le problème se résume à deux faits:

1. **Lorsque vous supprimez un noeud, chaque enfant devient un composant distinct dont la taille est égale à sa taille de sous-arbre. **
2. **Les nœuds restants (tous ceux qui ne sont pas dans aucun sous-arbre d'enfant) forment un composant de plus** – le «reste» de l'arbre.

Par conséquent, si vous connaissez la taille de chaque sous-arbre, vous pouvez calculer le score pour chaque noeud en un seul passage ascendant.

---

Aperçu de la solution
Nous construisons une liste d'adjacence (« enfants ») et effectuons un DFS post-commande qui retourne la taille du sous-arbre enraciné dans le nœud actuel.

Pendant le DFS:

1. Pour chaque enfant `c`, calculer récursivement `size_c`.
2. Multipliez le produit courant (`score`) par `size_c`.
3. Cumuler `total += size_c`.
4. Après avoir exploré tous les enfants, le nombre de nœuds restants est
"rest = n - total - 1".
5. Si `rest > 0`, multipliez `score` par `rest`.
6. Suivre le score maximum vu jusqu'à présent et compter combien de nœuds l'ont frappé.

Tous les arithmétiques utilisent des entiers 64 bits («long»/«long long») pour éviter les débordements.

---

Analyse de complexité

Étape Coût
- Oui.
Liste des bâtiments d'appoint Autres
(chaque nœud visité une fois)
Mémoire **O(n)** (liste des dépendances + pile de récursion)

Ainsi, la solution globale fonctionne dans **O(n)** temps et **O(n)** espace – le meilleur pour ce problème.

---

Nombre d'implémentations linguistiques spécifiques

- Oui. 1. Java
"Java
Importation de java.util.*;

solution de classe {
Nombre d'entrées publiquesHighestScoreNodes(int[] parents) {
int n = parents.longueur;
Liste <entier>[] enfants = nouvelle liste de répartition;
pour (int i = 0; i < n; i++) les enfants[i] = nouvelle liste de distribution<>();
pour (int i = 1; i < n; i++) enfants[parents[i]].add(i);

long[] maxScore = nouveau long[1]; // tableau d'utilisation pour permettre une modification dans lambda imbriquée
réponse int[] = nouvelle int[1];

// DFS post-commande mis en œuvre par une méthode privée
int dfs(int node) {
long score = 1;
= 0;
pour (int enfant : enfants[node]) {
int sz = dfs(enfant);
score *= sz;
somme += sz;
}
repos int = n - somme - 1;
si (rest > 0) score *= repos;

si (score > maxScore[0]) { maxScore[0] = score; réponse[0] = 1; }
Sinon si (score == maxScore[0]) { réponse[0]++; }

somme de retour + 1;
}

dfs(0);
réponse de retour[0];
}
}
«» "

- Oui. 2. Python
'`python
de taper l'importation Liste

Solution de classe:
def countHighestScoreNodes(self, parents: List[int]) -> Int:
n = len(parents)
enfants = [[] pour _ dans l'intervalle(n)]
pour i dans la plage (1, n):
enfants[parents[i]].annexe(i)

auto.max_score = 0
réponse = 0

def dfs(node: int) -> Int:
score = 1
Total = 0
pour les enfants[node]:
sz = dfs(enfant)
score *= sz
Total += sz
repos = n - total - 1
en cas de repos > 0:
score *= repos
si score > self.max_score:
auto.max_score = score
réponse = 1
score elif == self.max_score:
réponse += 1
total de retour + 1

dfs(0)
Revenez vous-même. réponse
«» "

- Oui. 3. C++
'`cpp
solution de classe {
public:
nombre intHighestScoreNodes(vecteur<int> et parents) {
int n = parents.size();
vecteur<vecteur<int>> enfant(n);
pour (int i = 1; i < n; ++i) enfant[parents[i]].push_back(i);

long maxScore = 0;
réponse int = 0;

fonction<int(int)> dfs = [&](inint node) -> Int {
long score = 1;
= 0;
pour (int ch : enfant[node]) {
int sz = dfs(ch);
score *= sz;
somme += sz;
}
repos int = n - somme - 1;
si (rest > 0) score *= repos;

si (score > maxScore) { maxScore = score; réponse = 1; }
Sinon, si (score == maxScore) { ++réponse; }

somme de retour + 1;
};

dfs(0);
réponse de retour;
}
};
«» "

---

Pourquoi Cette solution Rocks

Pourquoi ça compte ?
- Oui.
**Temps linéaire**=Les intervieweurs aiment O(n) – cela montre que vous comprenez la traversée de l'arbre. Autres
**Séparation claire des préoccupations** Autres
**Arithmétique sûr**= L'utilisation de `long / long` prévient le débordement sur 2 × 105 nœuds. Autres
**Post-order traversal**S'assure que les tailles de sous-arbres sont connues avant de calculer une partition de parent. Autres
**Tracking de l'état sur place**= Pas besoin d'un tableau auxiliaire pour stocker tous les scores – nous mettons à jour `maxScore` et `result` à la volée. Autres

---

Les erreurs communes qui vous font perdre des points

Erreurs d'impact
- C'est quoi ?
Utiliser `int` pour le score= Dépassement → mauvaises réponses= Passer à `long` (`long long` en C++/Java)=
Oublier `-1` lors du calcul `rest`
Ne pas manipuler `rest = 0` (racine) Pas de problème.
Pré-commander le DFS sans mémoriser Les enfants ne sont pas encore traités → taille du sous-arbre manquant
Ignorer la limite de la pile de récursions

---

## Le "Ugly" – Des motifs de mess qui mènent aux bogues

Motif Pourquoi il est laid
- C'est quoi ?
Bâtiment `reste` en tant que `n - total` (oubliant `-1`)
Récursion retournant une paire `(taille, score)` Suringénierie; boucles à deux couches
Autres Stocker toutes les tailles de composants dans un vecteur séparé.
Utiliser des variables globales sans encapsulation

---

La dernière sortie
LeetCode 2049 est plus qu'une question astucieuse – il vous oblige à penser **aux conséquences de couper un noeud**. Maîtrisez le tour O(n) DFS, évitez les pièges de débordement, et vous impressionnerez à la fois le gestionnaire de location et le tableau noir algorithmique.

> **Pro‐Tip**: Lors de la pratique, essayez d'écrire la solution en deux** langues (p. ex. Java & Python). Il vous forme à traduire des idées algorithmiques à travers les écosystèmes – une compétence vitale lors de l'entretien de rôles qui utilisent des piles technologiques hétérogènes.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

*Pour des plongées plus profondes dans des problèmes d'arbres ou d'autres défis d'entrevue LeetCode, abonnez-vous à notre newsletter et continuez à coder! *

---

> **Auteur**: *[Votre nom]* – passionné de codage, avocat d'algorithmes et ingénieur logiciel de première année se préparant à un portefeuille d'entrevues.

---

> **Contact**: `youremail@example.com`" `LinkedIn: /in/votreprofil`" `GitHub: /votrenom d'utilisateur "

---

TL;DR
- O(n) DFS + taille du sous-arbre = solution optimale pour LeetCode 2049.
- Utilisez l'arithmétique 64 bits, manipulez soigneusement la racine et mettez à jour le score maximum à la volée.
- Oui. Le problème est une question d'entrevue stellaire: propre, évolutive, et pleine de nuance arithmétique subtile.

Joyeux entretien !

---

* Se sentir libre d'adapter l'extrait de blog dans votre propre plateforme de blog ou Linked En post pour présenter votre plongée profonde dans **LeetCode 2049**. *

---

** Fin du poste**.